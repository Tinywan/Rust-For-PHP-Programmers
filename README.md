# Rust for PHP Programmers 🦀 🐘

> 面向 PHP 开发者的 Rust 进阶指南：从动态弱类型到编译期安全，从 Shared-Nothing 到高并发常驻内存。

本项目参考微软官方 Rust 培训体系（Bridge 桥接系列），专门为拥有 PHP 8+ / Laravel / Symfony / Swoole / RoadRunner 背景的工程师打造，帮助 PHP 开发者平滑跨越心智断层，掌握生产级 Rust 开发，并利用 Rust 赋能 PHP 生态（如开发高性能原生扩展与微服务 Sidecar）。

---

## 📖 核心目标与读者痛点

- **突破性能天花板**：解决 CPU 密集型计算、复杂数据序列化、音视频流媒体处理、AI 本地推理场景下的性能与内存瓶颈。
- **重塑内存心智模型**：从 PHP 的 Zend GC（引用计数与循环垃圾收集）无缝过渡到 Rust 的编译期所有权（Ownership）与借用检查（Borrow Checker）。
- **常驻内存与真正并发**：从 PHP-FPM 单请求隔离生命周期，进阶到 Tokio 异步运行时与多线程共享状态。
- **PHP 与 Rust 协同实战**：学会使用 ext-php-rs 编写纯 Rust 的安全 PHP 原生扩展，或通过 FFI 高速互调，无需推翻现有业务架构即可获取极致性能提升。

---

## 🗺️ 核心知识映射（Mental Model Bridge）

| 领域 / 概念 | PHP（PHP 8+） | Rust | 核心心智转换 |
| :--- | :--- | :--- | :--- |
| **执行模型** | 经典 Shared-Nothing，单请求生命周期 | 单一长期运行进程，共享内存 / 消息传递并发 | 摆脱 请求结束即销毁，显式掌控资源生命周期 |
| **类型系统** | 动态类型 + 渐进类型（Union Types 等） | 编译期静态强类型 + 智能类型推导 | 杜绝运行时隐式转换与隐藏类型异常 |
| **空值与异常** | 
ull、	ry/catch、Throwable | Option<T>、Result<T, E>、? 语法糖 | 将异常视为正常控制流转为编译期强制显式处理错误 |
| **内存与安全** | Zend GC（zval 结构体与引用计数） | 所有权系统（Move 语义 + 借用规则） | 零运行时 GC 开销，编译期杜绝空指针与数据竞争 |
| **结构建模** | class、extends 继承、interface、	rait | struct、enum（可携带数据）、impl、	rait | 告别类继承体系，拥抱数据结构与行为解耦的组合模式 |
| **核心数据容器** | 万能关联数组 rray | Vec<T>、HashMap<K, V>、切片 &[T] 等 | 告别一个 Array 走天下，根据内存布局选择高效数据结构 |
| **依赖与包管理** | Composer (composer.json / Packagist) | Cargo (Cargo.toml / crates.io) | 心智高度相似，极速上手 |
| **原生扩展** | C 语言 Zend API（易段错误、易泄漏） | ext-php-rs 编写安全扩展 / C-ABI 动态库 FFI | 用类型安全的现代语言重构 PHP 底层扩展 |

---

## 📚 目录路线图（Book Outline）

### 第一部分：心智重塑与极速上手（The Mindset Shift）
- **01. 为什么 PHP 开发者需要学习 Rust？**
- **02. 工具链对齐**：从 composer 到 cargo，从 php.ini 到 Cargo.toml
- **03. 告别 Shared-Nothing**：理解常驻内存世界的生存法则

### 第二部分：核心语法与范式蜕变（Syntax & Paradigms）
- **04. 告别万能 Array**：Rust 数据结构体系（Vec、HashMap、Slice）与内存布局
- **05. 从面向对象继承到 Trait 组合**：Struct + Impl + Trait 实战
- **06. 告别 try/catch 与 null**：Option<T>、Result<T, E> 与生产级错误处理
- **07. 突破最大心理关**：深度理解所有权（Ownership）与借用检查（Borrow Checker）

### 第三部分：并发与常驻服务（Concurrency & Runtime）
- **08. 从 PHP-FPM 多进程到 Tokio 异步多线程**
- **09. 跨线程状态共享与安全通信**：Arc<Mutex<T>> 与 Channel 模式

### 第四部分：PHP 与 Rust 双剑合璧（Interop & Extension）
- **10. 现代 PHP 扩展开发利器**：使用 ext-php-rs 编写原生扩展
- **11. 跨语言调用**：通过 PHP 8 FFI 直接调用 Rust C-ABI 动态链接库
- **12. 微服务架构与 Sidecar 模式**：PHP 敏捷交付 + Rust 性能卫士

### 第五部分：生产实战演练（Production Engineering）
- **13. 测试与基准分析**：从 PHPUnit 到 cargo test 与 criterion
- **14. 极致轻量的容器化部署**：打造小于 10MB 的 Scratch 生产镜像

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
