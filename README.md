# Rust for PHP Programmers 🦀 🐘

> 面向 PHP 开发者的 Rust 进阶指南：从动态弱类型到编译期安全，从 Shared-Nothing 到高并发常驻内存。

本项目参考微软官方 Rust 培训体系（Bridge 桥接系列），专门为拥有 **PHP 8+ / Laravel / Symfony / Workerman / Webman / Swoole / RoadRunner** 背景的工程师打造，帮助 PHP 开发者平滑跨越心智断层，掌握生产级 Rust 开发，并利用 Rust 赋能 PHP 生态（如开发高性能原生扩展与微服务 Sidecar）。

---

## 📖 核心目标与读者痛点

- **突破性能天花板**：解决 CPU 密集型计算、复杂数据序列化、音视频流媒体处理、AI 本地推理场景下的性能与内存瓶颈。
- **重塑内存心智模型**：从 PHP 的 Zend GC（引用计数与循环垃圾收集）无缝过渡到 Rust 的编译期所有权（Ownership）与借用检查（Borrow Checker）。
- **常驻内存与真正并发**：从 PHP-FPM 单请求隔离生命周期，进阶到 Tokio 异步运行时与多线程共享状态。
- **PHP 与 Rust 协同实战**：学会使用 `ext-php-rs` 编写纯 Rust 的安全 PHP 原生扩展，或通过 FFI 高速互调，无需推翻现有业务架构即可获取极致性能提升。

---

## 🗺️ 核心知识映射（Mental Model Bridge）

| 领域 / 概念 | PHP（PHP 8+） | Rust | 核心心智转换 |
| :--- | :--- | :--- | :--- |
| **执行模型** | 经典 Shared-Nothing，单请求生命周期 | 单一长期运行进程，共享内存 / 消息传递并发 | 摆脱“请求结束即销毁”，显式掌控资源生命周期 |
| **类型系统** | 动态类型 + 渐进类型（Union Types 等） | 编译期静态强类型 + 智能类型推导 | 杜绝运行时隐式转换与隐藏类型异常 |
| **空值与异常** | `null`、`try/catch`、`Throwable` | `Option<T>`、`Result<T, E>`、`?` 语法糖 | 将异常视为正常控制流转为“编译期强制显式处理错误” |
| **内存与安全** | Zend GC（zval 结构体与引用计数） | 所有权系统（Move 语义 + 借用规则） | 零运行时 GC 开销，编译期杜绝空指针与数据竞争 |
| **结构建模** | `class`、`extends` 继承、`interface`、`trait` | `struct`、`enum`（可携带数据）、`impl`、`trait` | 告别类继承体系，拥抱数据结构与行为解耦的组合模式 |
| **核心数据容器** | 万能关联数组 `array` | `Vec<T>`、`HashMap<K, V>`、切片 `&[T]` 等 | 告别一个 Array 走天下，根据内存布局选择高效数据结构 |
| **依赖与包管理** | `Composer` (`composer.json` / Packagist) | `Cargo` (`Cargo.toml` / crates.io) | 心智高度相似，极速上手 |
| **原生扩展** | C 语言 Zend API（易段错误、易泄漏） | `ext-php-rs` 编写安全扩展 / C-ABI 动态库 FFI | 用类型安全的现代语言重构 PHP 底层扩展 |

---

## 📚 目录路线图（Book Outline）

### 第一部分：基础语法与心智重塑（The Mindset Shift）
- **01. 动机与破局：为什么学习 Rust？**
- **02. 快速起步：Composer 与 Cargo**
- **03. 变量与类型：从弱类型到静态确定性**
- **04. 流程控制与表达式块**
- **05. 集合与容器：告别万能 Array**
- **06. 枚举与模式匹配：代数数据类型**

### 第二部分：突破心智关与语言特性（Paradigms & Core Mechanics）
- **07. 所有权与借用：从 zval 理解生命周期**
- **08. 组织与模块：从 PSR-4 到 Module Tree**
- **09. 错误处理：告别 try/catch 与 null**
- **10. 特征与泛型：Trait 并非代码混入**
- **11. 类型转换：From 与 Into 显式契约**
- **12. 闭包与迭代器：函数式特性的进化**

### 第三部分：高性能并发与生态融合（Concurrency & Ecosystem Interop）
- **13. 并发编程：PHP-FPM 到 Tokio 异步多线程**
- **14. 扩展开发：ext-php-rs 编写原生扩展**
- **15. 架构演进：PHP 与 Rust 协同模式**
- **16. 最佳实践与罗塞塔石碑速查**
- **17. 综合实战：打造高性能应用网关**

---

## 📄 详细方案与规划

完整实施路线图与设计文档请查阅：[PLAN.md](./PLAN.md)。

---

## 🤝 参与贡献

欢迎对 PHP 和 Rust 充满热情的小伙伴共同完善本教程！
- 提交 Issue 探讨章节内容或提出你在学习 Rust 时的困惑；
- 提交 PR 贡献示例代码或优化文档表述。

## 📜 许可协议

MIT License.
