# Money

The `Money` type represents an amount of money in a specified currency.

## Schema

A `Money` has two fields:

- The `currency_code` field is a string containing a currency code.

  The three-letter currency codes defined in the ISO 4217 standard are always
  supported.

  APIs may define additional currency codes that are not included in ISO 4217
  (for example, virtual currencies or cryptocurrencies). These must start with
  with "X-", in order to distinguish them from potential future ISO 4217 codes.

  Examples:

  - "USD" - ISO 4217 code for United States dollar
  - "X-BTC" - Potential API-defined extension for Bitcoin.
  - "X-.RBX" - Potential API-defined extension for the virtual currency Robux

- The `amount` field is a field of type [`Decimal`][], representing the amount
  of currency.

## Examples

- Five US dollars === `{currency_code: "USD", amount: {significand: 5}}`
- One and a half Bitcoin ===
  `{currency_code: "X-BTC", amount: {significand: -5, exponent: -3}}`

<!--prettier-ignore-start-->
[`Decimal`]: ./decimal.md
<!--prettier-ignore-end-->
