# Introduction

## Introduction

Vif is a system programming language aimed at game development. It specifically targets data-oriented programming. Vif is still very young, so this document may be incomplete or not properly reflect the upstream state of the language.

Its main inspirations are Odin, Zig, and Rust, the language started as being very Zig-based and was iterated upon. The syntax and semantics may feel very similar to Zig.

## Bonjour, Vif!

```vif
extern "c" fn printf(fmt: *const u8, ...) i32;

const slice = @import("std").slice;

fn main() void {
    printf(slice.ptr("Bonjour, Vif!"));
}
```

```shell
$ vifc run main.vif
Bonjour!
```
A program entry point is a function named `main` returning `void` inside the root module. 

The `std.slice.ptr` helper is currently used to pass string data to C-style APIs.

## Module

A module is a Vif file. Each module is also an implicit `struct`, like Zig.

The root module is the main module which the semantic analysis is started from.

The Vif compiler ships with special modules that you can `@import`  everywhere:
- `std`: the Vif standard library
- `builtin`: built-in language and compiler types
- `root`: the root module

## Comments

Line comments start with `//`.

```vif
// This is a comment.
const x = 10;
```
