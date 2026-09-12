# 02. 快速起步：Composer 与 Cargo 的双重视角

> “如果你熟悉 Composer，恭喜你，你已经理解了 Cargo 80% 的工作机制。”

对于现代 PHP 开发者来说，`Composer` 几乎是日常工作的核心——我们每天都在与 `composer.json`、`composer.lock`、`Packagist` 打交道。

而 Rust 的官方包管理器与构建工具 **Cargo**，被公认为当今软件工业界设计最优雅的工具链之一。更令人惊喜的是，Cargo 的心智模型与 Composer 高度相似。

本章我们将通过双重视角对比，带你快速完成 Rust 工具链的搭建，创建你的第一个工程，并理解二者的映射关系。

---

## 1. 工具链安装与版本管理

在 PHP 世界中，我们通常使用系统包管理器（如 Ubuntu 的 `apt`、Mac 的 `brew`）或者专门的工具（如 `phpbrew`、Docker）来管理 PHP 版本。

而在 Rust 生态中，官方提供了统一的工具链管理器：**`rustup`**。

### 安装 Rust 工具链
打开终端运行官方推荐脚本：
- **Linux / macOS**:
  ```bash
  curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
  ```
- **Windows**:
  访问 [https://rustup.rs/](https://rustup.rs/) 下载 `rustup-init.exe` 并按照提示安装即可（推荐默认的 MSVC 工具链）。

### 验证安装
安装完成后，在终端中输入：
```bash
rustc --version  # 查看 Rust 编译器版本
cargo --version  # 查看 Cargo 包管理器版本
```

> [!TIP]
> `rustup` 不仅可以安装 Rust，还支持一键升级（`rustup update`）以及切换不同的发行通道（`stable` 稳定版 / `nightly` 开发版）。

---

## 2. Composer vs Cargo：核心概念一一映射

让我们直观对比两个生态中的概念对应关系：

| 维度 | PHP (Composer) | Rust (Cargo) | 机制差异说明 |
| :--- | :--- | :--- | :--- |
| **包管理器命令** | `composer` | `cargo` | Cargo 同时还兼任**编译构建器**与**测试运行器** |
| **项目依赖声明** | `composer.json` | `Cargo.toml` | Cargo 采用 TOML 语法，比 JSON 更简洁并原生支持注释 |
| **精确版本锁定** | `composer.lock` | `Cargo.lock` | 机制完全一致：锁定依赖的具体 Git Hash 与发布版本 |
| **公共镜像源** | [Packagist.org](https://packagist.org) | [crates.io](https://crates.io) | 社区官方托管的包仓库 |
| **依赖术语** | Package / 库 | **Crate（箱）** | Rust 中的每个第三方依赖被称为一个 Crate |
| **本地依赖缓存** | `~/.composer/cache` + 项目下 `vendor/` | `~/.cargo/registry` + 项目下 `target/` | Rust 不会把源码直接拷贝到项目里，编译产物统一放在 `target/` |

---

## 3. 创建你的第一个 Rust 项目

在 PHP 中，我们通常使用 `composer init` 来初始化一个项目；而在 Rust 中，使用 `cargo new`。

### 步骤 1：新建一个可执行二进制项目
```bash
cargo new hello_rust
cd hello_rust
```

观察 Cargo 自动生成的目录结构：
```text
hello_rust/
├── Cargo.toml          # 类似 composer.json
├── .gitignore          # 自动配置忽略 target/ 目录
└── src/
    └── main.rs         # 类似 public/index.php，程序入口
```

### 步骤 2：剖析 `Cargo.toml`
打开 `Cargo.toml`，内容非常清爽：
```toml
[package]
name = "hello_rust"
version = "0.1.0"
edition = "2021"

[dependencies]
# 类似 composer.json 中的 "require" 区块
```

### 步骤 3：编写代码 (`src/main.rs`)
打开 `src/main.rs`，Cargo 已经为我们生成了经典的问候代码：
```rust
fn main() {
    println!("Hello, World from Rust!");
}
```

- `fn main()` 是可执行程序的入口函数；
- `println!` 是一个宏（Macro），以感叹号结尾，用于格式化输出字符串并自动换行。

### 步骤 4：编译与运行
在 PHP 中，我们直接执行 `php index.php`；而 Rust 是静态编译型语言，需要先编译后执行。Cargo 将这两步合二为一：
```bash
cargo run
```
控制台将输出：
```text
   Compiling hello_rust v0.1.0 (D:\AI\Rust-For-PHP-Programmers\examples\hello_rust)
    Finished dev [unoptimized + debuginfo] target(s) in 0.42s
     Running `target/debug/hello_rust.exe`
Hello, World from Rust!
```

---

## 4. 引入第三方依赖：以处理时间为例

在 PHP 中，如果我们想处理复杂时间，我们会执行：
```bash
composer require nesbot/carbon
```

在 Rust 中，我们使用著名的 `chrono` crate。我们可以直接通过命令行添加：
```bash
cargo add chrono
```
此时打开 `Cargo.toml`，你会发现它自动多了一行：
```toml
[dependencies]
chrono = "0.4"
```

修改 `src/main.rs`：
```rust
use chrono::Local;

fn main() {
    let now = Local::now();
    println!("当前本地时间是: {}", now.format("%Y-%m-%d %H:%M:%S"));
}
```

再次运行 `cargo run`，Cargo 会自动从 `crates.io` 下载 `chrono` 及其所有子依赖、完成静态编译，并直接输出当前时间！

---

## 5. 开发调试 vs 生产发布构建

在 PHP 中，我们上线代码通常只需要部署代码文件并开启 OPcache。

而 Rust 程序在本地开发和生产上线时有明确的构建模式区分：

1. **开发构建（Debug 模式，默认）**：
   - 命令：`cargo build` 或 `cargo run`
   - 特点：编译速度快，包含大量调试符号（Debug Info），未开启指令优化。
   - 产物路径：`target/debug/hello_rust`

2. **生产构建（Release 模式）**：
   - 命令：`cargo build --release`
   - 特点：编译器开启最高级别的优化（内联、死代码消除、LTO 跨模块链接优化），编译速度相对较慢，但**运行性能通常比 Debug 模式快 10 到 100 倍**！
   - 产物路径：`target/release/hello_rust`（可以直接拷贝到生产服务器独立运行的二进制可执行文件）。

> [!IMPORTANT]
> **切记**：在对 Rust 代码进行任何基准性能测试（Benchmark）或对比 PHP 性能时，**务必带上 `--release` 参数**！千万不要用 Debug 构建产物去测速度。

---

## 本章小结

- Rust 的 `rustup` 让工具链安装和版本升级变得非常优雅；
- `Cargo` 是集包管理、构建、测试与运行于一体的一站式工具，其 `Cargo.toml` 和 `Cargo.lock` 的使用体验与 `composer` 几乎完全对应；
- 通过 `cargo run` 可以一键体验从编译到执行的全流程，生产环境切记使用 `cargo build --release` 生成极致优化的静态二进制文件。

下一章：**[03. 变量、可变性与核心类型：从弱类型到静态确定性](ch03-built-in-types-and-variables.md)**，我们将正式进入 Rust 的语法世界，探讨变量、类型系统与内存绑定的第一课！
