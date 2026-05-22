# Directives

Directives begin with `#`. They modify declarations, types, or operations without introducing new keywords.

## Expressions

### `#inline` and `#noinline`

Force or not a function or function call to be inlined.

```vif
#inline fn id(value: i32) i32 {
    return value;
}
```

### `#linear`

Mark a value expression as *linear* which gives it linear value sematnics.

### `#packed`

Remove any padding between fields of a `struct`. 

Useful for bitfields structs.

```vif
#packed struct D3D12_RAYTRACING_INSTANCE_DESC {
    transform: Mat3x4,
    instance_id: u24,
    instance_mask: u8,
    instance_contribution_to_hit_group_index: u24,
    flags: u8,
    acceleration_structure: u64,
}
```

### `#callconv(<cc>)`

Change the *calling convention* of a function.

`<cc>` must be of type `builtin.CallingConvention`

```vif
fn foo() #callconv(.c) void;
```

### `#addrspace(<space>)`

TODO

### `#volatile`

TODO