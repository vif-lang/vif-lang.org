# Literals

## Boolean Literals

```vif
const yes = true;
const no = false;
```

## Integer Literals

Integer literals may be decimal, hexadecimal, binary, or octal.

```vif
const decimal = 1234;
const hex = 0xff;
const binary = 0b1010;
const octal = 0o755;
```

Integer literals can use type suffixes.

```vif
const a = 1usize;
const b = 2i32;
const c = 255u8;
```

Untyped integer literals are represented as compile-time integer values (with the `anyint` type) until a concrete type is required, in which case implicit coercion is performed.

```vif
const a = 20;       // compile-time integer
const b: u8 = 20;   // implicitly coerced to u8
```

## Float Literals

Floating point literals use a decimal point or exponent.

```vif
const x = 1.0;
const y = 1.0e9;
const z = 2.5f32;
```

The scalar floating types are `f16`, `f32`, `f64`, and `f128`.

Like untyped integer literals, untyped floating point literals are represented with the `anyfloat` type.