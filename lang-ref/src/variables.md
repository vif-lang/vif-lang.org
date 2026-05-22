# Variables

A variable represent some memory location containing a value with a certain type. 

Shadowing of variable is permitted.

```vif
// Declares `a` of type `i32` with the value `20`
const a: i32 = 20;

// Declares `a` of type `anyint` with the value `20`.
// The type can be omitted and inferred from the initializing expression. 
// In the case of integer literals, the inferred type is `anyint` unless a explicit type suffix is provided.  
const a = 20;
```

You can also use the `var` keyword instead of `const` to create a **mutable** variable, the main recommandation is to use `const` by default unless mutability is preferred / needed. `const` conveys to the reader and tools that the variable is not meant to be mutated.

## Comptime

Marking a variable with `comptime` makes the variable compile-time only, making its value known and computed at compilation. See more at TODO.
