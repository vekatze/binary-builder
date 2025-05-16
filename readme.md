# binary-builder

`binary-builder` is a Neut library to construct binary data efficiently.

## Installation

```sh
neut get binary-builder https://github.com/vekatze/binary-builder/raw/main/archive/0-1-25.tar.zst
```

## Types

### Basics

```neut
inline builder: type

// Allocates memory of size `size` and returns it as a builder.
// The builder's size automatically doubles when there is
// insufficient space to append new data.
define make-builder(size: int): builder

// Extracts the accumulated binary data from the builder.
define extract(b: builder): binary
```

### Builders

#### Texts and Binaries

```neut
// Appends the text `x` to the builder `b`.
define append-text(b: &builder, x: &text): unit

// Appends the binary `x` to the builder `b`.
define append-binary(b: &builder, x: &binary): unit
```

#### Integers

```neut
// Appends int64 to the given builder as binary.
define append-int64(b: &builder, x: int64): unit

// Appends int64 to the given builder as UTF-8 text.
define append-int64-UTF8(b: &builder, x: int64): unit

// An int32 variant of `append-int64`.
define append-int32(b: &builder, x: int32): unit

// An int32 variant of `append-int64-UTF8`.
define append-int32-UTF8(b: &builder, x: int32): unit

// An int16 variant of `append-int16`.
define append-int16(b: &builder, x: int16): unit

// An int16 variant of `append-int64-UTF8`.
define append-int16-UTF8(b: &builder, x: int16): unit

// Appends int8 to the given builder as binary.
define append-int8(b: &builder, x: int8): unit

// Appends int8 to the given builder as UTF-8 text.
define append-int8-UTF8(b: &builder, x: int8): unit
```

#### Floats

```neut
// Appends float64 to the given builder as binary.
define append-float64(b: &builder, x: float64): unit

// Appends float64 to the given builder as UTF-8 text.
define append-float64-UTF8(b: &builder, x: float64): unit

// An float32 variant of `append-float64`.
define append-float32(b: &builder, x: float32): unit

// An float32 variant of `append-float64-UTF8`.
define append-float32-UTF8(b: &builder, x: float32): unit

// An float16 variant of `append-float64`.
define append-float16(b: &builder, x: float16): unit

// An float16 variant of `append-float64-UTF8`.
define append-float16-UTF8(b: &builder, x: float16): unit
```

## Example

```neut
define zen(): unit {
  let b = make-builder(4) in
  let _ on b =
    append-text(b, "hello");
    append-int64-UTF8(b, 123);
    append-text(b, "world")
  in
  let result = extract(b) in
  printf("{}\n", [_Text(result)])
}

// => hello123world
```
