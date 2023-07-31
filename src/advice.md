# 其他风格建议

## 表达式

尽可能使用 Rust 面向表达式的特性；

```rust,ignore
// 使用
let x = if y { 1 } else { 0 };
// 不使用
let x;
if y {
    x = 1;
} else {
    x = 0;
}
```

## 命名规范

- 类型应为首字母大写的驼峰命名法（`UpperCamelCase`），
- 枚举变量应为首字母大写的驼峰命名法（`UpperCamelCase`），
- 结构体字段应使用纯小写下划线命名法（`snake_case`），
- 函数和方法名称应使用纯小写下划线命名法（`snake_case`），
- 局部变量应为纯小写下划线命名法（`snake_case`），
- 宏名称应为纯小写下划线命名法（`snake_case`），
- 常量（常量和不可变静态）应使用纯大写下划线命名（`SCREAMING_SNAKE_CASE`）
- 当名称是保留字（如 `crate`）而禁止使用时，要么使用原始标识符（`r#crate`），要么使用尾部下划线（`crate_`）——不要拼错单词 (`krate`)。

### 模块

尽可能避免使用 `#[path]` 标注。
