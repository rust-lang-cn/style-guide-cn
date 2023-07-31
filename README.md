# Rust 语言风格指南

![Build Status](https://github.com/rust-lang-cn/style-guide-cn/workflows/CI/badge.svg)
[![LICENSE-MIT](https://img.shields.io/badge/license-MIT-green)](https://raw.githubusercontent.com/rust-lang-cn/style-guide-cn/master/LICENSE-MIT)
[![LICENSE-APACHE](https://img.shields.io/badge/license-Apache%202-blue)](https://raw.githubusercontent.com/rust-lang-cn/style-guide-cn/master/LICENSE-APACHE)
[![GitHub last commit](https://img.shields.io/github/last-commit/rust-lang-cn/style-guide-cn?color=gold)](https://github.com/rust-lang-cn/style-guide-cn/commits/master)
[![GitHub contributors](https://img.shields.io/github/contributors/rust-lang-cn/style-guide-cn?color=pink)](https://github.com/rust-lang-cn/style-guide-cn/graphs/contributors)
![Locatized 100%](https://img.shields.io/badge/localized-100%25-purple)
[![rustwiki.org](https://img.shields.io/website?up_message=rustwiki.org&url=https%3A%2F%2Frustwiki.org)](https://rustwiki.org)

> The Chinese Translation of [The Rust Style Guide][style-guide-en]
>
> - 首次于 2023-07-31 翻译完全部内容，欢迎纠正——最后更新时间 2023-07-31。
> - 期待更多朋友加入 [Rust 中文翻译项目组](https://github.com/rust-lang-cn)，协助我们，一起更新完善中文版，感激不尽！

这是《Rust 语言风格指南》中文版，翻译自 [Rust 源码中的《The Rust Style Guide》][style-guide-src]。

在线版可在本组织官网上阅读，包括[全球站点][style-guide-cn]或[国内站点][style-guide-cn-zh]（**均支持同一页面中英双语切换**）,或者在 Rust 官网上[阅读英文版][style-guide-en]。

[style-guide-src]: https://github.com/rust-lang/rust/tree/master/src/doc/style-guide
[style-guide-cn]: https://rustwiki.org/zh-CN/style-guide/
[style-guide-cn-zh]: https://www.rustwiki.org.cn/zh-CN/style-guide/
[style-guide-en]: https://doc.rust-lang.org/style-guide/

## 构建

构建之前请先安装 `mdBook` 工具。

从 GitHub 下载仓库并构建：

```sh
$ git clone https://github.com/rust-lang-cn/style-guide-cn.git
$ cd style-guide-cn
$ mdbook serve
```

然后就可以在浏览器上访问 `http://localhost:3000` 来查看文档内容了。

要生成本地图书，使用以下命令：

```sh
$ mdbook build
```

即可在当前仓库目录下生存一个 `book` 子目录，可找到相应的 HTML 文件。

## 许可协议

《Rust 语言风格指南》（中文版与英文版 *The Rust Style Guide* 均） 使用以下两种协议的任一种进行授权：

- Apache 2.0 授权协议，（[LICENSE-APACHE](LICENSE-APACHE) 或 http://www.apache.org/licenses/LICENSE-2.0）
- MIT 授权协议 ([LICENSE-MIT](LICENSE-MIT) 或 http://opensource.org/licenses/MIT)

可以根据自己选择来定。

除非您有另外说明，否则您在本仓库提交的任何贡献均按上述方式进行双重许可授权，就如 Apache 2.0 协议所规定那样，而无需附加任何其他条款或条件。
