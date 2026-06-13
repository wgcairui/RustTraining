# Rust 核心术语表（中英对照）

> 来源：microsoft/RustTraining 中文翻译项目维护。
> 译法参考：[Rust 语言中文社区](https://rustcc.cn/)、[Rust 程序设计语言（简体中文版）](https://rustwiki.org/zh-CN/book/)、[Rust Reference 中文译本](https://rustwiki.org/)。
>
> **使用约定**：
> - 第一次出现某术语时，用 `**中文（English）**` 格式 + 一句话定义
> - 后续出现直接用中文（或英文，看哪种更顺）
> - 新术语发现后请 PR 补充到这里

---

## A · 基础概念

| 中文 | English | 一句话解释 |
|---|---|---|
| 所有权 | ownership | 每个值有且仅有一个所有者（owner），所有者离开作用域时值被释放 |
| 移动 | move | 把值的所有权从一个变量转移给另一个变量，原变量失效 |
| 复制 | copy | 在栈上按位复制一份（要求类型实现 `Copy` trait） |
| 克隆 | clone | 显式深拷贝一份堆数据（`clone()` 方法） |
| 借用 | borrowing | 通过引用（reference）使用值，不取得所有权 |
| 不可变引用 | shared reference / `&T` | 只读借用，多个可同时存在 |
| 可变引用 | mutable reference / `&mut T` | 可写借用，同时刻只能存在一个 |
| 引用 | reference | 借用值的"句柄"，不拥有数据 |
| 解引用 | dereference | 通过 `*` 操作符从引用拿到值 |
| 解引用强制转换 | deref coercion | 自动把 `&T` 转成 `&U` 当 `T: Deref<Target=U>` |

---

## B · 类型系统

| 中文 | English | 一句话解释 |
|---|---|---|
| 静态类型 | statically typed | 编译期确定每个变量的类型 |
| 类型推断 | type inference | 编译器自动推导类型，无需显式标注 |
| 泛型 | generics | 参数化类型，写一次代码适用多种类型 |
| trait | trait | Rust 的"接口/抽象能力"机制，定义类型能做什么 |
| 实现 | impl（implementation） | 为某个类型实现 trait 或方法 |
| 结构体 | struct | Rust 的"类"，三种子类型：普通结构体、元组结构体、单元结构体 |
| 枚举 | enum | Rust 的"和类型（sum type）"，可承载不同变体 |
| 模式匹配 | pattern matching | 用 `match`、解构等语法按形状匹配值 |
| 穷尽匹配 | exhaustive matching | `match` 必须覆盖所有可能，否则编译报错 |
| 关联类型 | associated type | trait 里用 `type Item` 定义的占位类型 |
| 关联函数 | associated function | 关联在类型上的函数，类似静态方法 |
| 方法 | method | 第一个参数是 `self` 的关联函数 |
| Trait 约束 / Trait bound | trait bound | 泛型上的"必须有某 trait"约束（`T: Display`） |
| Trait 对象 | trait object / `dyn Trait` | 运行时多态，类型擦除 |
| 静态分派 | static dispatch | 编译期决定调哪个方法（泛型 + 单态化） |
| 动态分派 | dynamic dispatch | 运行期通过 vtable 决定调哪个方法（trait 对象） |

---

## C · 内存与生命周期

| 中文 | English | 一句话解释 |
|---|---|---|
| 栈 | stack | 后进先出的连续内存，存定长数据，分配释放极快 |
| 堆 | heap | 运行时动态分配的内存，存不定长数据 |
| 生命周期 | lifetime | 引用保持有效的作用域，编译期静态检查 |
| 生命周期注解 | lifetime annotation | 显式标注 `'a` 让编译器知道多个引用的关系 |
| 析构 / drop | drop | 变量离开作用域时自动调用的清理逻辑 |
| 析构函数 | drop function / `Drop::drop` | 实现 `Drop` trait 的方法 |
| 泄漏 | leak | 内存没被释放且永远无法释放 |
| 移动语义 | move semantics | 赋值默认转移所有权（不像 C# 是复制引用） |
| 零成本抽象 | zero-cost abstraction | 抽象在编译期被消除，运行时无额外开销 |

---

## D · 错误处理

| 中文 | English | 一句话解释 |
|---|---|---|
| `panic!` | panic | 不可恢复错误，线程开始 unwind 栈 |
| `Result<T, E>` | Result | 可恢复错误的返回类型，`Ok(T)` / `Err(E)` |
| `Option<T>` | Option | 可空值的类型，`Some(T)` / `None` |
| `?` 操作符 | `?` operator | 错误早返：如果是 `Err` 直接返回，否则解包 `Ok` |
| 错误传播 | error propagation | 把错误沿调用栈向上抛 |
| unwrap | unwrap | `Result` / `Option` 的便捷取值法，遇 `Err`/`None` 直接 panic |
| expect | expect | 同 unwrap，但带自定义 panic 消息 |

---

## E · 模块与包

| 中文 | English | 一句话解释 |
|---|---|---|
| crate | crate | Rust 的编译单元，可以是 binary 或 library |
| package | package | `Cargo.toml` 描述的一个或多个 crate 的集合 |
| 模块 | module | 用 `mod` 组织的代码块，控制可见性 |
| 路径 | path | 引用模块 / 类型 / 函数的写法（绝对 / 相对） |
| `use` | use | 把路径引入当前作用域 |
| `pub` | pub | 标记项为对外可见 |
| Cargo | Cargo | Rust 的构建工具和包管理器 |
| 工作空间 | workspace | 多个共享 `Cargo.lock` 的 package 集合 |

---

## F · 并发与异步

| 中文 | English | 一句话解释 |
|---|---|---|
| 线程 | thread | OS 线程，Rust 标准库 `std::thread` |
| 通道 | channel | `mpsc::channel()`，线程间消息传递 |
| `Send` | Send | 标记 trait：类型可以跨线程移动所有权 |
| `Sync` | Sync | 标记 trait：类型可以跨线程共享引用 |
| 互斥锁 | mutex | `std::sync::Mutex`，同一时刻只允许一个线程访问 |
| 异步 | async | 协作式并发，不阻塞 OS 线程 |
| `.await` | await | 挂起点，让运行时调度其他任务 |
| Future | future | 一个"将来某刻产出值"的值，惰性 |
| 运行时 | runtime | 异步任务的执行器（如 tokio、async-std） |
| Tokio | Tokio | 最主流的 Rust 异步运行时 |
| 任务 | task | 运行时调度的基本单位，对应一次 `spawn` |
| 串行执行器 | single-threaded executor | 一次只跑一个任务（如 `current_thread`） |
| 多线程执行器 | multi-threaded executor | 任务跑在多个工作线程上（如 `tokio::runtime::Runtime`） |
| 取消安全 | cancellation safety | Future 被 drop 时是否破坏一致性 |

---

## G · 宏与元编程

| 中文 | English | 一句话解释 |
|---|---|---|
| 宏 | macro | 编译期代码生成，写法上分声明宏（`macro_rules!`）和过程宏 |
| 派生宏 | derive macro | `#[derive(Debug)]` 这种给类型自动实现 trait |
| 属性 | attribute | `#[...]` 形式的注解 |

---

## H · 不安全 Rust

| 中文 | English | 一句话解释 |
|---|---|---|
| 不安全 Rust | unsafe Rust | 关闭部分编译期检查的子集（unsafe block / fn / trait） |
| 裸指针 | raw pointer | `*const T` / `*mut T`，不受借用检查器保护 |
| FFI | FFI（Foreign Function Interface）| 调用 C / 其他语言库 |
| `extern "C"` | extern block | 声明外部 ABI 函数 |

---

## I · 与 C# 对照

> 专为本翻译项目（C# → Rust）准备的对照表。

| C# 概念 | Rust 对应 | 备注 |
|---|---|---|
| class | struct + impl | Rust 没有继承，靠 trait + 组合 |
| interface | trait | 概念最接近 |
| `record` | struct + `#[derive(Clone, Copy, PartialEq)]` | 真正的不可变 |
| `async` / `await` | `async` / `.await` | Rust 是惰性的，必须有运行时驱动 |
| `Task<T>` | `Future<Output = T>` | 概念类似但 Rust 不自带调度 |
| `Task.Run(...)` | `tokio::spawn(...)` | 启动并发任务 |
| `lock` / `Monitor` | `std::sync::Mutex` / `tokio::sync::Mutex` | 异步场景必须用 tokio 版的锁 |
| `null` / `Nullable<T>` | `Option<T>` | Rust 无 null |
| `try/catch` | `Result<T, E>` + `?` | Rust 没有异常，错误是值 |
| `using var` / `IDisposable` | `Drop` trait | 离开作用域自动清理 |
| `IEnumerable<T>` | `Iterator` trait | Rust 迭代器是惰性的 |
| `LINQ` | 迭代器适配器 | `map` / `filter` / `collect` |
| NuGet | crates.io + Cargo | 包管理 |
| `IL` / JIT | LLVM AOT | 编译模型 |
| GC | 无（编译期管理）| Rust 无 GC |

---

## J · 译者注

- `trait` 不译是中英文社区共识，强行译"特征"反而难懂
- `crate` 译"包"会和 Rust 的"package"（Cargo package）混淆，保留英文更清楚
- `enum` 译"枚举"是 C# 习惯，但 Rust enum 比 C# 强太多，译"枚举"会低估，建议第一次出现加 `(sum type)` 注解
- `Self` / `self` 不译，区别大小写是 Rust 语义的一部分