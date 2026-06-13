# 翻译规范（Translation Conventions）

> 本规范是 microsoft/RustTraining 中文翻译版的统一标准，所有译者请遵守。
> 适用范围：`csharp-book-zh/`、`async-book-zh/` 等所有 `*-book-zh/` 平行目录。

---

## 1. 文件与目录约定

- **平行目录**：每本英文书的翻译版放在 `xxx-book-zh/`，不动原版结构
- **章节文件名保持英文**：`ch07-ownership-and-borrowing.md` 不改成 `ch07-所有权与借用.md`，方便：
  - 与上游同步（diff 友好）
  - 内部 `../chapter.md` 链接不需要改
  - 路径里没中文，避免某些工具链问题
- **SUMMARY.md 标题中文化**，但文件名不动
- **不翻译章节里的外部链接**，原样保留；如果是 GitHub anchor，加一行注释说明对应章节
- **新增内容**（如译者注、术语表引用）放在原文段落之后，用 HTML 注释包裹

---

## 2. 术语翻译原则

### 2.1 一律"中文（English）"首次出现格式

专有名词第一次出现时，**中文 + 英文 + 解释**：

> **所有权（ownership）**：Rust 中每个值都有一个所有者（owner），所有者离开作用域时值被自动释放。

后续出现直接用中文即可。

### 2.2 优先复用既有中文 Rust 社区译法

参考已有中文 Rust 资料的常用译法，避免生造词：

| 英文 | 推荐中文 | 不推荐 |
|---|---|---|
| ownership | 所有权 | 归属权 |
| borrowing | 借用 | 借用权 |
| lifetime | 生命周期 | 生命期 |
| trait | trait（不译） | 特征 |
| crate | crate（不译）| 包 |
| borrow checker | 借用检查器 | 借用检查程序 |
| move semantics | 移动语义 | 转移语义 |
| zero-cost abstraction | 零成本抽象 | 无开销抽象 |
| pattern matching | 模式匹配 | 模式匹配 |
| enum | 枚举 | 枚举类型 |
| match | match（不译） | 匹配 |
| struct | 结构体 | 结构 |
| impl | impl（不译） | 实现块 |
| deref coercion | 解引用强制转换 | 解引用强制 |
| drop | 析构 / drop（不译） | 丢弃 |
| mutable | 可变 | 可修改 |
| immutable | 不可变 | 不可修改 |
| shadowing | 遮蔽（shadowing） | 隐藏 |
| slice | 切片（slice） | 片 |
| reference | 引用 | 引用类型 |
| raw pointer | 裸指针 | 原始指针 |
| smart pointer | 智能指针 | — |
| Send / Sync | `Send` / `Sync`（不译）| — |

完整版见 [`glossary.md`](./glossary.md)。

### 2.3 不译的情况

- **关键字**：`fn`、`let`、`mut`、`pub`、`mod`、`use`、`struct`、`enum`、`impl`、`trait`、`match`、`if`、`else`、`while`、`for`、`loop`、`return`、`as`、`in`、`where`、`Self`、`self`
- **类型名**：`String`、`Vec`、`Option`、`Result`、`Box`、`Rc`、`Arc`、`Cell`、`RefCell`
- **Trait 名**：`Iterator`、`IntoIterator`、`From`、`Into`、`Display`、`Debug`、`Clone`、`Copy`、`Default`、`Drop`、`Send`、`Sync`
- **标准库函数**：`println!`、`format!`、`vec!`、`panic!`
- **crate 名**：`serde`、`tokio`、`actix-web`、`axum`
- **crate 命令**：`cargo`、`rustc`、`rustup`、`mdbook`
- **错误类型 / 错误消息**：编译错误原文照搬，加中文翻译注释

---

## 3. 代码块规则

### 3.1 代码块完全不译

```rust
fn main() {
    let mut s = String::from("hello");
    s.push_str(", world");
    println!("{}", s);
}
```

代码、注释（用 `//`）、输出都不译。**注释也是代码的一部分**，保留英文是让读者日后查官方文档不卡壳。

### 3.2 代码块**上方或下方**的解释文字可以译

代码块前的引导段、后的解读段，全译。

### 3.3 行内代码、文件名、命令保持原样

- `Vec<T>` 不译成 `向量<T>`
- `cargo build` 不译
- 文件名 `main.rs` 不译

---

## 4. 链接与锚点

### 4.1 内部相对链接不动

`[第 7 章](../ch07-ownership-and-borrowing/ch07.md)` 这种内部链接**不译**，因为文件名没改。

### 4.2 外部链接保留英文

`https://doc.rust-lang.org/book/...` 不译。

### 4.3 加锚点中文化提示（可选）

如果原章节用 anchor 链接到小节，可在译文章节末尾加一个"译者注"区块：

```html
<!-- translator-note -->
> 译者注：原文用 `#mutable-bindings` 作为锚点，本译文小节标题改为「`mut` 绑定」后可在浏览器复制 anchor。
<!-- /translator-note -->
```

---

## 5. Mermaid 图

- 图里的**英文文本**（节点标签、边标签）保留英文，**图下方说明**翻译
- 例外：图本身就是表达核心概念、且中文阅读明显顺畅的（比如流程图），可译，但要在图下注明「图已翻译为中文」

---

## 6. Playground / 可执行代码块

保持原样。Playground 是 Rust 官方 playground，代码必须英文。

---

## 7. Commit / 署名

每个 commit message 建议格式：

```
[zh] csharp-book: ch07 所有权与借用

- 初译完成
- 术语已校对（参考 docs-zh/glossary.md）

译者：cairui
```

`[zh]` 前缀方便过滤。commit author 用你自己的，不冒充原作者。

---

## 8. 翻译进度标记

每章开头加一行进度标记，方便维护：

```markdown
<!-- translation-status: draft | review | done -->
<!-- last-updated: 2026-06-13 -->
```

---

## 9. 不译的部分（保留原样）

- 标题里的英文人名 / 项目名
- 书名引用（如"The Rust Programming Language"）
- 引用块（`>` 开头）—— 引用外部资料时保留原文，加译者注说明出处

---

## 10. 校对流程（建议）

1. 自翻：`draft`
2. 跑 `mdbook serve` 本地通读一遍，检查 mermaid 图、链接、代码块
3. 找一段对照原文比对术语 → `review`
4. 提交 PR → `done`