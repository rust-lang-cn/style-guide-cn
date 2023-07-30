# 语句

## `let` 语句

在 `:` 后面和 `=` 的两边（若它们存在的话）空一格。分号前不要空格。

```rust
// 一条注释。
let pattern: Type = expr;

let pattern;
let pattern: Type;
let pattern = expr;
```

如果可能，将声明格式化成一行。如果不可能，则在 `=` 之后尝试分割，如果声明适合在两行中进行。将表达式块缩进。

```rust
let pattern: Type =
    expr;
```

如果第一行仍不能排在一行上，则在 `:` 之后分行，并使用块缩进。即使在 `:` 后分行后类型还需要多行，也应将第一行放在与 `:` 相同的行上，并遵守[合并规则](expressions.html#combinable-expressions)。

```rust
let pattern:
    Type =
    expr;
```

例如：

```rust
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

```rust
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

### else blocks (let-else statements)

A let statement can contain an `else` component, making it a let-else statement.
In this case, always apply the same formatting rules to the components preceding
the `else` block (i.e. the `let pattern: Type = initializer_expr` portion)
as described [for other let statements](#let-statements).

Format the entire let-else statement on a single line if all the following are
true:

* the entire statement is *short*
* the `else` block contains only a single-line expression and no statements
* the `else` block contains no comments
* the let statement components preceding the `else` block can be formatted on a single line

```rust
let Some(1) = opt else { return };
```

Otherwise, the let-else statement requires some line breaks.

If breaking a let-else statement across multiple lines, never break between the
`else` and the `{`, and always break before the `}`.

If the let statement components preceding the `else` can be formatted on a
single line, but the let-else does not qualify to be placed entirely on a
single line, put the `else {` on the same line as the initializer expression,
with a space between them, then break the line after the `{`. Indent the
closing `}` to match the `let`, and indent the contained block one step
further.

```rust
let Some(1) = opt else {
    return;
};

let Some(1) = opt else {
    // nope
    return
};
```

If the let statement components preceding the `else` can be formatted on a
single line, but the `else {` does not fit on the same line, break the line
before the `else`.

```rust
    let Some(x) = some_really_really_really_really_really_really_really_really_really_long_name
    else {
        return;
    };
```

If the initializer expression is multi-line, put the `else` keyword and opening
brace of the block (i.e. `else {`) on the same line as the end of the
initializer expression, with a space between them, if and only if all the
following are true:

* The initializer expression ends with one or more closing
  parentheses, square brackets, and/or braces
* There is nothing else on that line
* That line has the same indentation level as the initial `let` keyword.

For example:

```rust
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

Otherwise, put the `else` keyword and opening brace on the next line after the
end of the initializer expression, with the `else` keyword at the same
indentation level as the `let` keyword.

For example:

```rust
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

## Macros in statement position

For a macro use in statement position, use parentheses or square brackets as
delimiters, and terminate it with a semicolon. Do not put spaces around the
name, `!`, the delimiters, or the `;`.

```rust
// A comment.
a_macro!(...);
```


## Expressions in statement position

Do not put space between the expression and the semicolon.

```
<expr>;
```

Terminate all expressions in statement position with a semicolon, unless they
end with a block or are used as the value for a block.

E.g.,

```rust
{
    an_expression();
    expr_as_value()
}

return foo();

loop {
    break;
}
```

Use a semicolon where an expression has void type, even if it could be
propagated. E.g.,

```rust
fn foo() { ... }

fn bar() {
    foo();
}
```
