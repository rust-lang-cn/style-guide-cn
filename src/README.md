# Rust 语言风格指南

## 动机——为什么要使用格式化工具？

格式化代码是一项耗时耗力的机械性工作。如果使用自动格式化工具，开发者就可以从这项工作中解脱出来，专注于更重要的事情。

此外，通过坚持使用既定的风格指南（如本指南），开发者无需制定特别的风格规则，也无需与其他开发者争论应使用何种样式规则，从而节省了时间、沟通成本和精神耗损。

人类通过模式匹配来理解信息。通过确保所有 Rust 代码具有相似的格式，就能减少理解新项目所需的脑力劳动，从而降低新开发人员的入门门槛。

因此，使用格式化工具（如 `rustfmt`）可以提高工作效率，而使用社区一致的格式规约（通常是使用格式化工具的默认设置）则会带来更大的好处。

## 默认 Rust 风格

《Rust 语言风格指南》定义了默认 Rust 风格，并**建议**开发者和工具遵循默认 Rust 样式。`rustfmt` 等工具使用此风格指南作为默认风格的参考。本风格指南中的所有内容，无论是否使用“必须”等语言或“插入空格......”或“在......后换行”等命令式语气，都是指默认样式。

这不应被解释为禁止开发人员遵循非默认样式，或禁止工具添加任何特定的配置选项。

## 格式约定

### 缩进和行宽

- 使用空格，而不是制表符。
- 每级缩进必须是 4 个空格（也就是说，字符串字面量和注释之外的所有缩进空格数都必须是 4 的倍数）。
- 一行的最大宽度为 100 个字符。

#### 块缩进

与视觉化缩进（visual indent）相比，更倾向于分块缩进：

```rust
// 块缩进
a_function_call(
    foo,
    bar,
);

// 视觉化缩进
a_function_call(foo,
                bar);
```

这样做的差异就会变小（例如，在上例中重命名了`a_function_call`），向右移动的情况也会减少。

### Trailing commas

In comma-separated lists of any kind, use a trailing comma when followed by a
newline:

```rust
function_call(
    argument,
    another_argument,
);

let array = [
    element,
    another_element,
    yet_another_element,
];
```

This makes moving code (e.g., by copy and paste) easier, and makes diffs
smaller, as appending or removing items does not require modifying another line
to add or remove a comma.

### Blank lines

Separate items and statements by either zero or one blank lines (i.e., one or
two newlines). E.g,

```rust
fn foo() {
    let x = ...;

    let y = ...;
    let z = ...;
}

fn bar() {}
fn baz() {}
```

### [Module-level items](items.md)
### [Statements](statements.md)
### [Expressions](expressions.md)
### [Types](types.md)


### Comments

The following guidelines for comments are recommendations only, a mechanical
formatter might skip formatting of comments.

Prefer line comments (`//`) to block comments (`/* ... */`).

When using line comments, put a single space after the opening sigil.

When using single-line block comments, put a single space after the opening
sigil and before the closing sigil. For multi-line block comments, put a
newline after the opening sigil, and a newline before the closing sigil.

Prefer to put a comment on its own line. Where a comment follows code, put a
single space before it. Where a block comment appears inline, use surrounding
whitespace as if it were an identifier or keyword. Do not include trailing
whitespace after a comment or at the end of any line in a multi-line comment.
Examples:

```rust
// A comment on an item.
struct Foo { ... }

fn foo() {} // A comment after an item.

pub fn foo(/* a comment before an argument */ x: T) {...}
```

Comments should usually be complete sentences. Start with a capital letter, end
with a period (`.`). An inline block comment may be treated as a note without
punctuation.

Source lines which are entirely a comment should be limited to 80 characters
in length (including comment sigils, but excluding indentation) or the maximum
width of the line (including comment sigils and indentation), whichever is
smaller:

```rust
// This comment goes up to the ................................. 80 char margin.

{
    // This comment is .............................................. 80 chars wide.
}

{
    {
        {
            {
                {
                    {
                        // This comment is limited by the ......................... 100 char margin.
                    }
                }
            }
        }
    }
}
```

#### Doc comments

Prefer line comments (`///`) to block comments (`/** ... */`).

Prefer outer doc comments (`///` or `/** ... */`), only use inner doc comments
(`//!` and `/*! ... */`) to write module-level or crate-level documentation.

Put doc comments before attributes.

### Attributes

Put each attribute on its own line, indented to the level of the item.
In the case of inner attributes (`#!`), indent it to the level of the inside of
the item. Prefer outer attributes, where possible.

For attributes with argument lists, format like functions.

```rust
#[repr(C)]
#[foo(foo, bar)]
#[long_multi_line_attribute(
    split,
    across,
    lines,
)]
struct CRepr {
    #![repr(C)]
    x: f32,
    y: f32,
}
```

For attributes with an equal sign, put a single space before and after the `=`,
e.g., `#[foo = 42]`.

There must only be a single `derive` attribute. Note for tool authors: if
combining multiple `derive` attributes into a single attribute, the ordering of
the derived names must generally be preserved for correctness:
`#[derive(Foo)] #[derive(Bar)] struct Baz;` must be formatted to
`#[derive(Foo, Bar)] struct Baz;`.

### *small* items

In many places in this guide we specify formatting that depends on a code
construct being *small*. For example, single-line vs multi-line struct
literals:

```rust
// Normal formatting
Foo {
    f1: an_expression,
    f2: another_expression(),
}

// "small" formatting
Foo { f1, f2 }
```

We leave it to individual tools to decide on exactly what *small* means. In
particular, tools are free to use different definitions in different
circumstances.

Some suitable heuristics are the size of the item (in characters) or the
complexity of an item (for example, that all components must be simple names,
not more complex sub-expressions). For more discussion on suitable heuristics,
see [this issue](https://github.com/rust-lang-nursery/fmt-rfcs/issues/47).

## [Non-formatting conventions](advice.md)

## [Cargo.toml conventions](cargo.md)

## [Principles used for deciding these guidelines](principles.md)
