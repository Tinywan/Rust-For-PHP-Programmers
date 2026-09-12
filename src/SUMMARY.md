# Summary

[前言：写给 PHP 开发者的 Rust 进阶指南](introduction.md)

# Part I: 基础语法与心智重塑

- [01. 动机与破局：为什么 PHP 开发者需要学习 Rust？](ch01-introduction-and-motivation.md)
- [02. 快速起步：Composer 与 Cargo 的双重视角](ch02-getting-started.md)
- [03. 变量、可变性与核心类型：从弱类型到静态确定性](ch03-built-in-types-and-variables.md)
- [04. 流程控制与表达式块：告别语句式心智](ch04-control-flow.md)
- [05. 集合与数据容器：告别万能 Array 的时代](ch05-data-structures-and-collections.md)
- [06. 枚举与模式匹配：比 PHP 8 Enum 强大百倍的代数数据类型](ch06-enums-and-pattern-matching.md)

# Part II: 突破心智关与语言特性

- [07. 所有权与借用检查：从 PHP zval 垃圾回收理解生命周期](ch07-ownership-and-borrowing.md)
- [08. 组织架构与模块系统：从 PSR-4 到 Rust Module Tree](ch08-crates-and-modules.md)
- [09. 错误处理哲学：告别 try/catch 与隐式 null](ch09-error-handling.md)
- [10. 特征与泛型：Trait 并非 PHP 的代码片段混入](ch10-traits-and-generics.md)
- [11. 类型转换的标准范式：From、Into 与显式契约](ch11-from-and-into-traits.md)
- [12. 闭包与链式迭代器：函数式特性的终极进化](ch12-closures-and-iterators.md)

# Part III: 高性能并发与生态融合

- [13. 并发编程：从 PHP-FPM 多进程到 Tokio 异步多线程](ch13-concurrency.md)
- [14. 杀手级生态融合：使用 ext-php-rs 开发纯 Rust 原生扩展](ch14-unsafe-and-php-extensions.md)
- [15. 架构演进与渐进式重构：PHP 与 Rust 的协同作战模式](ch15-migration-patterns.md)
- [16. 生产最佳实践与罗塞塔石碑（PHP→Rust 速查手册）](ch16-best-practices-and-rosetta-stone.md)
- [17. 综合实战（Capstone Project）：打造高性能常驻进程应用网关](ch17-capstone-project.md)
