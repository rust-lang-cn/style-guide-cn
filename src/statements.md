# 语句

## `let` 语句

在 `:` 后面和 `=` 的两边（若它们存在的话）空一格。分号前不要空格。

```rust,ignore
// 一条注释。
let pattern: Type = expr;

let pattern;
let pattern: Type;
let pattern = expr;
```

如果可能，将声明格式化成一行。如果不可能，则在 `=` 之后尝试分割，如果声明适合在两行中进行。将表达式块缩进。

```rust,ignore
let pattern: Type =
    expr;
```

如果第一行仍不能排在一行上，则在 `:` 之后分行，并使用块缩进。即使在 `:` 后分行后类型还需要多行，也应将第一行放在与 `:` 相同的行上，并遵守[合并规则](expressions.html#combinable-expressions)。

```rust,ignore
let pattern:
    Type =
    expr;
```

例如：

```rust,ignore
let Foo {
    f: abcd,
    g: qwer,
}: Foo<Bar> =
    Foo { f, g };

let (abcd,
    defg):
    Baz =
{ ... }
```

如果表达式包含多行，若表达式的第一行适合在余下空位上，则表达式与 `=` 保留在同一行，表达式的其余部分不再缩进。如果第一行不合适，则将表达式放在后面的行中，分块缩进。如果表达式是一个代码块，且类型或模式覆盖多行，则将开头括号放在新的一行，且不缩进（这样可以将代码块内部与类型分开）；否则，开头括号放在 `=` 之后。

示例：

```rust,ignore
let foo = Foo {
    f: abcd,
    g: qwer,
};

let foo =
    ALongName {
        f: abcd,
        g: qwer,
    };

let foo: Type = {
    an_expression();
    ...
};

let foo:
    ALongType =
{
    an_expression();
    ...
};

let Foo {
    f: abcd,
    g: qwer,
}: Foo<Bar> = Foo {
    f: blimblimblim,
    g: blamblamblam,
};

let Foo {
    f: abcd,
    g: qwer,
}: Foo<Bar> = foo(
    blimblimblim,
    blamblamblam,
);
```

### else 块（let-else 语句）

一个 let 语句可以包含一个 `else` 组件，使其成为一个 let-else 语句。在这种情况下，应始终对 else 块前面的组件（即 `let pattern: Type = initializer_expr` 部分）采用与[其他 let 语句](#let-语句)相同的格式化规则。

如果以下条件都符合，则将整个 let-else 语句格式化为一行：

- 整个语句很**短**
- `else` 块只包含一个单行表达式，不包含任何语句
- `else` 块不包含注释
- `else` 块前面的 let 语句组件可以格式化为单行

```rust,ignore
let Some(1) = opt else { return };
```

否则，let-else 语句需要换行。

如果将 let-else 语句换成多行，切勿在`else` 和 `{` 之间换行，一定要在 `}` 之前换行。

如果 `else` 前面的 let 语句组件可以格式化为一行，但 let-else 不符合完全放在一行的条件，则应将 `else {` 放在初始化表达式的同一行，并在两者之间留一个空格，然后在 `{` 之后换行。缩进结尾的 `}` 以匹配 `let`，并将包含的代码块再缩进一步。

```rust,ignore
let Some(1) = opt else {
    return;
};

let Some(1) = opt else {
    // nope
    return
};
```

如果 `else` 前面的 let 语句组件可以在一行中格式化，但 `else {` 不能在同一行中格式化时，则在 `else` 之前换行。

```rust,ignore
    let Some(x) = some_really_really_really_really_really_really_really_really_really_long_name
    else {
        return;
    };
```

如果初始化表达式为多行，则在且仅在以下所有条件都符合的情况下，将 `else` 关键字和代码块的开头括号（即 `else {`）放在与初始化表达式结尾相同的行上，并在它们之间留一个空格：

- 初始化表达式以一个或多个结束括号、方括号和/或大括号结束
- 该行没有其他内容
- 该行的缩进级别与初始 `let` 关键字的缩进级别相同

例如：

```rust,ignore
let Some(x) = y.foo(
    "abc",
    fairly_long_identifier,
    "def",
    "123456",
    "string",
    "cheese",
) else {
    bar()
}
```

否则，将 `else` 关键字和开头括号放在初始化表达式结束后的下一行，`else` 关键字的缩进级别与 `let` 关键字的缩进级别相同。

例如：

```rust,ignore
fn main() {
    let Some(x) = abcdef()
        .foo(
            "abc",
            some_really_really_really_long_ident,
            "ident",
            "123456",
        )
        .bar()
        .baz()
        .qux("fffffffffffffffff")
    else {
        return
    };

    let Some(aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa) =
        bbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbbb
    else {
        return;
    };

    let LongStructName(AnotherStruct {
        multi,
        line,
        pattern,
    }) = slice.as_ref()
    else {
        return;
    };

    let LongStructName(AnotherStruct {
        multi,
        line,
        pattern,
    }) = multi_line_function_call(
        arg1,
        arg2,
        arg3,
        arg4,
    ) else {
        return;
    };
}
```

## 在语句位置使用宏

在语句位置使用宏时，使用圆括号或方括号作为分隔符，并以分号结束。请勿在名称、`!`、分隔符或 `;` 前后使用空格。

```rust,ignore
// 注释
a_macro!(...);
```

## 语句位置中的表达式

表达式和分号之间不要加空格。

```rust,ignore
<expr>;
```

用分号结束语句位置上的所有表达式，除非这些表达式以块结束或用作块的值。

例如：

```rust,ignore
{
    an_expression();
    expr_as_value()
}

return foo();

loop {
    break;
}
```

表达式为空类型时，即使可以传递，也要使用分号。例如：

```rust,ignore
fn foo() { ... }

fn bar() {
    foo();
}
```
