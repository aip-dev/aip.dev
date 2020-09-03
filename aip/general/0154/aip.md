# Resource freshness validation

APIs often need to validate that a client and server agree on the current state
of a resource before taking some kind of action on that resource. For example,
two processes updating the same resource in parallel could create a race
condition, where the latter process "stomps over" the effort of the former one.

ETags provide a way to deal with this, by allowing the server to send a
checksum based on the current content of a resource; when the client sends that
checksum back, the server can ensure that the checksums match before acting on
the request.

## Guidance

A resource **may** provide an `etag` header when retrieving a single resource
when it is important to ensure that the client has an up to date resource
before acting on certain requests:

```
200 OK
Content-type: application/json
ETag: "55cc0347-66fc-46c3-a26f-98a9a7d61d0e"
```

The etag field **must** be provided by the server on output, and values
**should** conform to [RFC 7232][].

**Note:** ETag values **should** include quotes as described in [RFC 7232][].
For example, a valid etag is `"foo"`, not `foo`.

If the service receives a request to modify a resource that includes an
`If-Match` header, the service **must** validate that the value matches the
current etag. If the `If-Match` header value does not match the etag, the
service **must** reply with an HTTP 412 error.

If the user omits the `If-Match` header, the service **should** permit the
request. However, services with strong consistency or parallelism requirements
**may** require users to send etags all the time and reject the request with an
HTTP 400 error in this case.

### Strong and weak etags

ETags can be either "strongly validated" or "weakly validated":

- A strongly validated etag means that two resources bearing the same etag are
  byte-for-byte identical.
- A weakly validated etag means that two resources bearing the same etag are
  equivalent, but may differ in ways that the service does not consider to be
  important.

Resources **may** use either strong or weak etags, as it sees fit, but
**should** document the behavior. Additionally, weak etags **must** have a `W/`
prefix as mandated by [RFC 7232][]:

```
200 OK
Content-type: application/json
ETag: W/"55cc0347-66fc-46c3-a26f-98a9a7d61d0e"
```

## Further reading

- For how to retry on errors in client libraries, see AIP-194.

## Changelog

- **2020-09-02**: Clarified that other errors may take precedence over
  `FAILED_PRECONDITION` for etag mismatches.
- **2020-09-02**: Add guidance for etags on request messages.
- **2019-09-23**: Changed the title to "resource freshness validation".

[rfc 7232]: https://tools.ietf.org/html/rfc7232#section-2.3
