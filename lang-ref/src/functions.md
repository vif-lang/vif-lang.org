# Functions

## Overview

Functions are declared with `fn`.

```vif
fn add(a: i32, b: i32) i32 {
    return a + b;
}

// The final expression in a block may be used as a value in places where the language expects a value:
fn answer() i32 {
    42
}

// `return` exits the current function:
fn clamp_to_zero(x: i32) i32 {
    if x < 0 {
        return 0;
    }
    return x;
}

// function call syntax
const c = add(20, 30);
```

Functions prefixed with `@` are reserved for built-in functions.

Functions and function calls can be parametrized by [directives](./directives.md).

## Comptime parameters


Compile-time parameters are marked with `comptime`. This allows *generic functions*, each different `comptime` value will instantiate a different function.

```vif
fn add_n(comptime N: usize, value: usize) usize {
    return value + N;
}

fn Allocator(comptime backing_allocator_ty: type, comptime block_size_in_bytes: usize) type {
	struct {
        // ..
    }
}
```

## C Variadics

Variadic functions are supported for external C declarations.
```vif
extern "c" fn printf(fmt: *const u8, ...) i32;
```
