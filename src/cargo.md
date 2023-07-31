# `Cargo.toml` 的约定

## 格式约定

使用与 Rust 代码相同的行宽和缩进。

在一个表块的最后一个键值对与下一表块的标题之间空一行。在表块标题和该表块中的键值对之间，或同一表块中的键值对之间，不要加空行。

除 `[package]` 表块外，按字母顺序排列各部分中的键名。将 `[package]` 表块放在文件的顶部；将 `name` 和 `version` 键按顺序放在该表块的顶部，接着除 `description` 外的其余键按字母顺序排列，最后是该表块的末尾的 `description`。

任何标准键名都不要使用引号，使用裸键。只有名称需要引号的非标准键才使用引号，并尽可能避免引入此类键名。详情请参见 [TOML 规范](https://toml.io/cn/v1.0.0#键名)。

在键和值之间的 `=` 前后各留一个空格。不要缩进任何键名；所有键名都从一行的开头开始。

对于包含多行的字符串值，如 crate 说明，应使用多行字符串（而不是换行符）。

对于数组值（如特性列表），如果合适，可将整个列表与键放在同一行。否则，使用分块缩进：在开头的方括号后加一个换行符，每个项缩进一级，每个项（包括最后一个项）后加一个逗号，最后一个项后将结尾的方括号放在一行的开头。

对于数组值（如特征列表），如果合适，可将整个列表与键放在同一行。否则，使用分块缩进：在开头的方括号后加一个换行符，每个项目缩进一级，每个项目（包括最后一个项目）后加一个逗号，最后一个项目后将结尾的方括号放在一行的开头。

```rust,ignore
some_feature = [
    "another_feature",
    "yet_another_feature",
    "some_dependency?/some_feature",
]
```

对于表值，例如带有路径的 crate 依赖关系，如果合适的话，使用大括号和逗号将整个表写在与键相同的行上。如果整个表格不能与关键字写在同一行，则应使用键值对将其分隔成一个单独的部分：

```toml
[dependencies]
crate1 = { path = "crate1", version = "1.2.3" }

[dependencies.extremely_long_crate_name_goes_here]
path = "extremely_long_path_name_goes_right_here"
version = "4.5.6"
```

## 元数据约定

作者列表（若有的话）应由字符串组成，每个字符串包含一个作者姓名，后面是置于尖括号内的电子邮件地址： `Full Name
<email@address>`。不应包含空电子邮件地址或没有电子邮件地址的姓名。(作者列表中也可以包含没有相关姓名的邮件列表地址）。

许可证字段必须包含有效的 [SPDX 表达式](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)，并使用有效的 [SPDX 许可证名称](https://spdx.org/licenses/)。(作为例外，根据普遍惯例，许可证字段可以使用 `/` 代替 ` OR `，例如 `MIT/Apache-2.0`）。

主页字段（若有的话）必须包含一个单独的 URL，包括协议（如 `https://example.org/`，而不只是 `example.org`）。

在描述字段中，按 80 列对文本进行换行。不要以 crate 的名称作为描述字段的开头（例如 "cratename is a ..."）；只需描述 crate 本身。如果提供的是多句描述，第一句应单独成行并概括 crate，就像电子邮件或提交信息的主题一样；随后的句子可以更详细地描述 crate。
