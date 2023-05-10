# Decimal

The `Decimal` type represents a decimal numeric value. It uses a non-floating
point representation in order to avoid precision errors.

## Schema

A `Decimal` represents a decimal number in a form similar to scientific
notation.

It has two fields:

- The `digits` field is a 64-bit integer representing the significant digits of
  the number.
- The `exponent` field is a 32-bit integer represesnting the position of the
  deicmal point within the value of the `digits` field; it is the power of ten
  to which `digits` should be raised.

  When this value is unset or `0`; in that case, the value of the `Decimal` is
  simply the value of `digits`.

  When the exponent is greater than 0, represents the number of trailing zeroes
  after the digits.

  When the exponent is less than 0, represents how many of the significant
  digits (and implicit leading zeroes, as needed) come after the decimal point.

The general formula for converting a `Decimal` to its numeric value is
`digits * 10^exponent`, where `*` represents multplication and `^` represents
exponentiation.

## Examples

- 17 === `{digits: 17, exponent: 0}` (or just `{digits: 17}`)
- -0.005 === `{digits: -5, exponent: -3}`
- 33.5 million === `{digits: 335, exponent: 5}`
- 11/8 === 1.375 === `{digits: 1375, exponent: -3}`
