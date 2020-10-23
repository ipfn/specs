# Primitives

IPFN has idea of primitives inspired by [ECMAScript](https://tc39.es/ecma262/).

## Struct

Struct, namespace – directory in a tree structure, `Object` in ECMAScript.

## Boolean

True of false.

## String

It is different from simple byte array.

### Encoding

Property most useful for inter-language operability and auto-generated code.

* `hex`
* `utf8`
* `utf16` — Basic `String` in ECMAScript
* `base64`

## Number

* `i8`, `u8` – Signed and Unsigned `8` bit integer
* `i16`, `u16` – Signed and Unsigned `16` bit integer
* `i32`, `u32` – Signed and Unsigned `32` bit integer
* `f16` – `16` bit floating point number (mixed precision)
* `f32` – `32` bit floating point number
* `f64` – `64` bit floating point number — Basic `Number` in ECMAScript

## BigInt

Dynamic size integer.
