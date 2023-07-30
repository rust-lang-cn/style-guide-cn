# Rust 语言风格指南

这是 《Rust 语言风格指南》中文版，翻译自英文原版[《The Rust Style Guide》][style-guide]。

[style-guide]: https://doc.rust-lang.org/beta/style-guide/index.html

## 构建

构建之前请先安装 `mdBook` 工具。

从 GitHub 下载仓库并构建：

```sh
$ git clone https://github.com/rust-lang-cn/style-guide-cn.git
$ cd rustc-cn
$ mdbook serve
```

然后就可以在浏览器上访问 `http://localhost:3000` 来查看文档内容了。

要生成本地图书，使用以下命令：

```sh
$ mdbook build
```

即可在当前仓库目录下生存一个 `book` 子目录，可找到相应的 HTML 文件。

## 许可协议

本项目遵循 MIT 或 Apache 2.0 协议。
