# binary-builder

## Installation

```sh
neut get binary-builder https://github.com/vekatze/binary-builder/raw/main/archive/0-1-10.tar.zst
```

## Summary

```neut
constant builder: type

define create(size: int): builder

define get(b: builder): binary

define append-int64-little-endian(b: &builder, x: int64): unit

define append-int64-big-endian(b: &builder, x: int64): unit

define append-int64-UTF8(b: &builder, x: int64): unit

define append-int32-little-endian(b: &builder, x: int32): unit

define append-int32-big-endian(b: &builder, x: int32): unit

define append-int32-UTF8(b: &builder, x: int32): unit

define append-int16-little-endian(b: &builder, x: int16): unit

define append-int16-big-endian(b: &builder, x: int16): unit

define append-int16-UTF8(b: &builder, x: int16): unit

define append-int8(b: &builder, x: int8): unit

define append-int8-UTF8(b: &builder, x: int8): unit

define append-float64-little-endian(b: &builder, x: float64): unit

define append-float64-big-endian(b: &builder, x: float64): unit

define append-float64-UTF8(b: &builder, x: float64): unit

define append-float32-little-endian(b: &builder, x: float32): unit

define append-float32-big-endian(b: &builder, x: float32): unit

define append-float32-UTF8(b: &builder, x: float32): unit

define append-float16-little-endian(b: &builder, x: float16): unit

define append-float16-big-endian(b: &builder, x: float16): unit

define append-float16-UTF8(b: &builder, x: float16): unit

define append-binary(b: &builder, x: &binary): unit

define append-text(b: &builder, x: &text): unit
```

## Example

```neut
define zen(): unit {
  let b = create(4) in
  let _ on b =
    append-text(b, "hello");
    append-int64-UTF8(b, 123);
    append-text(b, "world")
  in
  let result = get(b) in
  printf("{}\n", [_Text(result)])
}

// => hello123world
```

(`append-XXX` extends the buffer when necessary)
