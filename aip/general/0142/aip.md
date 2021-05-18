# Time and duration

Many services need to represent the concepts surrounding time. Representing
time can be challenging due to the intricacies of calendars and time zones, as
well as the fact that common exchange formats (such as JSON) lack a native
concept of time.

## Guidance

Fields representing time **should** use a `string` field with values conforming
to [ISO 8601][], such as `2012-04-21T11:00:00-0500`.

Services **may** use IDL-specific timestamps where applicable (such as
[`google.protobuf.Timestamp`][timestamp] in protocol buffers) provided that the
service converts values to ISO 8601 timestamp strings in JSON.

### Timestamps

Fields that represent an absolute point in time (independent of any time zone
or calendar) **should** use a `string` field with ISO 8601 values, and
**should** send values in UTC, with the `Z` time zone explicitly included.

These fields **should** have names ending in `_time`, such as `create_time` or
`update_time`. For array fields, the names **should** end in `_times` instead.

Many timestamp fields refer to an activity (for example, `create_time` refers
to when the applicable resource was created). For these, the field **should**
be named with the `{imperative}_time` form. For example, if a book is being
published, the field storing the time when this happens would use the
imperative form of the verb "to publish" ("publish") resulting in a field
called `publish_time`. Fields **should not** be named using the past tense
(such as `published_time`, `created_time` or `last_updated_time`).

### Durations

Fields that represent a span between two points in time (independent of any
time zone or calendar) **should** use a `string` field with ISO 8601 duration
values, such as `P3Y6M4DT12H30M5S`. The field name **should** end with
`_duration`.

Designators for zero values **may** be omitted in accordance with ISO 8601 (for
example: `PT12H` is sufficient to represent "12 hours"), but at least one
designator **must** be present (therefore, a zero duration is `PT0S` or `P0D`).

Services **may** use IDL-specific durations where applicable (such as
[`google.protobuf.Duration`][timestamp] in protocol buffers) provided that the
service converts values to ISO 8601 duration strings in JSON.

### Relative time segments

In some cases, it may be necessary to represent a time segment inside a stream.
In these cases, a ISO 8601 duration value **should** be used, and the field
name **should** end with `_offset`. To ensure that the meaning is clear, the
field **must** have a comment noting the point that the offset is relative to.

To illustrate this, consider a resource representing a segment of an audio
stream:

```typescript
interface AudioSegment {
  // The duration relative to the start of the stream representing the
  // beginning of the segment.
  startOffset: string;

  // The total length of the segment.
  segmentDuration: string;
}
```

### Civil dates and times

Fields that represent a calendar date or wall-clock time **should** use partial
ISO 8601 strings.

Fields representing civil dates **should** have names ending in `_date`, while
fields representing civil times or datetimes **should** have names ending in
`_time`.

### Compatibility

Occasionally, APIs are unable to use ISO 8601 strings for legacy or
compatibility reasons. For example, an API may conform to a separate
specification that mandates that timestamps be Unix timestamp integers.

In these situations, fields **may** use other types. If possible, the following
naming conventions apply:

- For integers, include the meaning (examples: `time`, `duration`, `delay`,
  `latency`) **and** the unit of measurement (valid values: `seconds`,
  `millis`, `micros`, `nanos`) as a final suffix. For example,
  `send_time_millis`.
- For strings, include the meaning (examples: `time`, `duration`, `delay`,
  `latency`) but no unit suffix.

In all cases, clearly document the expected format, and the rationale for its
use.

<!-- prettier-ignore-start -->
[duration]: https://github.com/protocolbuffers/protobuf/blob/master/src/google/protobuf/duration.proto
[iso 8601]: https://www.iso.org/iso-8601-date-and-time-format.html
[timestamp]: https://github.com/protocolbuffers/protobuf/blob/master/src/google/protobuf/timestamp.proto
<!-- prettier-ignore-end -->
