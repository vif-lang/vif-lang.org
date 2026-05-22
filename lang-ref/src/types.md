# Types

## Primitive Types

```vif
bool

usize u8 u32 u64 u128   // unsigned integers
isize i8 i32 i64 i128   // signed integers

f16 f32 f64 f128        // floats

void                    // unit type
never                   // type of unreachable expressions (return, break, @unreachable)
Self                    // type of the current namespace owner

// comptime only types
anyint                  // type of a integer literal
anyfloat                // type of a float literal
type                    // type of a type (struct, enum, `i32`, ...)
```
Like Zig, Vif support bit-width integers: `i7` or `u4500` are supported. The maximum allowed bit-width is `65536`.

## Pointers

Pointers use the `*T` syntax.

```vif
var value: i32 = 10;
var ptr: *i32 = &value;
```

Const pointers use `*const T`.

```vif
extern "c" fn puts(text: *const u8) i32;
```

## Slices 

A slice represent a range of memory and packs together a pointer and a length.

```vif
const slice = @import("std").slice;

const str: []const u8 = "hello"; // string literals are slices of u8
slice.ptr(str);
slice.len(str); // 5
```

## Arrays

Arrays use `[N]T`.

```vif
var bytes: [16]u8 = @zeroed();
```

## Structs

Structs group named fields and declarations.

```vif
const Student = struct {
    age: i32,
    grade: i32,

    // functions, like all declarations, can be nested inside structs
    pub fn passes(student: Self) bool {
        return student.grade >= 10;
    }
};

// struct are initialized with the `.name = value` syntax
// each field must be initialized
const s = Student { .age = 22, .grade = 1 };

// you can access fields and declarations using the dot syntax
const age = s.age; // 22
const passes = Student.passes(s);
```

Structs can be parametrized by [directives](./directives.md) to e.g remove padding.

## Enums

Enums define named variants with declarations.

```vif
// if omitted, the enum tag type is computed by the compiler to fit the largest variant
// this enum tag type will `u2`
const Color = enum {
    Red,
    Green,
    Blue,
};

// initialization
const red = Color.Red;
const green: Color = .Green;

// explicit tag type
const Token = enum(u8) {
    Eof = 0,    // having a explicit value for a variant requires a explicit tag type
    Ident = 1,

    // like structs, enums can have declarations
    pub fn is_valid(tok: Self) bool {
        return token != Self.Eof;
    } 
};
```

## Unions

Unions implement tagged and untagged sum types.

```vif
// tagged union with a auto-generated tag type
const Item = union(enum) {
    apple,
    sword: i32,
};

const item = Item { .sword = 200 };

// using a switch you can switch over the tag and extract the variant value
switch item {
    .apple => {
        // holding an apple
    }
    .sword => |power| {
        // holding a sword with 200 power!
    }
}

// you can also create C-like (untagged) unions
const VkClearColorValue = union {
    float32: [4]f32,
    int32: [4]i32,
    uint32: [4]u32,
};

// TODO: example with a user-defined enum as a tag
```
