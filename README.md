# Javaboy

## 广大的javaboy无敌！！

[!image:45b9bd098b6c85fe9947c6509d7c732a.jpg]

### 让 Java 开发者读懂 Python、JavaScript、Go、Rust、SQL 和各种配置脚本

<p>
  <img src="https://img.shields.io/badge/OpenAI_Codex_CLI-412991?style=flat-square&logo=openai&logoColor=white" alt="OpenAI Codex CLI">
  <img src="https://img.shields.io/badge/Agent_Skills-SKILL.md-blue?style=flat-square" alt="Agent Skills">
  <img src="https://img.shields.io/badge/For-Java_Developers-orange?style=flat-square&logo=openjdk&logoColor=white" alt="For Java Developers">
  <img src="https://img.shields.io/badge/Language-中文-green?style=flat-square" alt="Chinese">
  <img src="https://img.shields.io/badge/License-MIT-green?style=flat-square" alt="MIT License">
</p>

> 不是把所有语言都讲成 Java，而是用 Java 开发者熟悉的心智模型，帮你准确理解陌生代码。

**Javaboy** 是一个面向 Java 开发者的 Codex Skill。它会在解释非 Java 代码时，先讲清源语言本身的真实语义，再映射到 Java 语法、JVM 习惯、Java 标准库、Spring 分层设计和类型模型。

适合这些场景：

1. 你是 Java 开发者，但项目里混着 Python、JavaScript、Shell、SQL、YAML。
2. 你能看懂一点语法，但不确定这段代码在运行时到底发生了什么。
3. 你想知道“如果用 Java 的方式理解，它大概像什么”。
4. 你在做跨语言迁移、代码审查、脚本维护或架构理解。

## 在线效果

你可以直接把陌生代码贴给 Codex，并要求：

```text
用 javaboy 的方式解释这段 Python，按 Java 开发者能理解的方式讲。
```

或者更直接：

```text
$javaboy
解释这段代码：
...
```

## 真实案例：Python 入口函数解释

面对这段 Python：

```python
if __name__ == '__main__':
    print_hi(demo_1())
```

普通解释可能只会说：直接运行文件时执行 `print_hi(demo_1())`。

Javaboy 会补上 Java 开发者需要的迁移理解：

```java
public static void main(String[] args) {
    printHi(demo1());
}
```

并明确指出：

- `__name__ == '__main__'` 类似 Java 程序入口判断，但不是完全等价的 `main` 方法。
- Python 文件被直接运行时，`__name__` 才是 `__main__`。
- 如果该文件被其他模块 `import`，这段代码不会自动执行。
- `print_hi(demo_1())` 的执行顺序是先调用 `demo_1()`，再把返回值传给 `print_hi(...)`。

## 问题：Java 开发者读陌生代码的五个卡点

| 卡点 | 表现 |
|------|------|
| 只懂字面语法 | 能猜出大概意思，但不知道运行时行为 |
| 类型模型错位 | 把 Python tuple、JS object、Go struct 直接套成 Java class |
| 异步模型混淆 | 把 Promise、async/await、goroutine、channel 都当成 Java Future |
| 错误处理误读 | 把 Go 的错误返回、Rust 的 Result、Python 异常混成一种机制 |
| 框架边界不清 | 看不出 controller、service、repository、middleware 对应关系 |

## 触发场景

### 自动触发

当你询问这些内容时，Javaboy 适合自动介入：

- 解释 Python、JavaScript、TypeScript、Go、Rust、Shell、SQL、YAML 等非 Java 代码。
- 把陌生语法映射到 Java 写法。
- 阅读脚本、配置、构建文件或接口调用流程。
- 分析非 Java 项目的模块边界、服务分层和数据流。
- 对比源语言写法和 Java 写法的语义差异。

### 手动触发

在 Codex 对话中输入：

```text
$javaboy
```

也可以自然语言触发：

```text
用 Java 开发者能理解的方式解释这段代码。
```

## 机制详解

### 四步解释法

| 步骤 | 内容 |
|------|------|
| 1. 源语言行为 | 先说明代码在原语言里实际做了什么 |
| 2. 语法特性 | 点出对应语法、标准库、框架习惯或运行时规则 |
| 3. Java 类比 | 给出最接近的 Java 写法、伪代码或设计类比 |
| 4. 语义差异 | 提醒 Java 开发者容易误解的地方 |

### Java 类比地图

| 源语言概念 | Java 视角 |
|-----------|-----------|
| Python `list` / JS `Array` | `List<T>` 或数组，但可变性和类型约束不同 |
| Python `dict` / JS object | `Map<K,V>`、DTO、record 或普通对象，取决于语义 |
| Python tuple | 轻量不可变序列，可类比 `record`，但字段通常没有名字 |
| JS Promise | 可类比 `CompletableFuture`，但调度和错误传播不同 |
| Go error return | 显式返回值检查，不是 Java 异常机制 |
| Rust Result | 类型系统表达成功/失败，不等于 try/catch |
| YAML / TOML / JSON | 配置数据，可类比 Spring 配置或 DTO 映射 |
| SQL result set | 关系数据，不是对象图，除非 ORM 做了映射 |

### 输出风格

Javaboy 默认使用紧凑、分块的解释方式：

````markdown
这段做了三件事：

1. `source_code_here`
   含义：...
   Java 类比：
   ```java
   Java example here
   ```
   注意：...
````

代码密集时，它会按函数、模块或业务流程分组，避免一次性把所有细节堆在一起。

## 示例：Python 坐标解析

源代码：

```python
start_parts = raw_task.start_node.data[0].split("_")
start_coord = (int(start_parts[0]), int(start_parts[1]), int(start_parts[2]))
target_loc = f"{start_coord[0]}_{start_coord[1]}_{start_coord[2]}"
```

Javaboy 会这样解释：

- `split("_")` 表示按 `_` 拆分字符串。Java 中类似 `String.split("_")`。
- `int(...)` 把字符串转成整数。Java 中类似 `Integer.parseInt(...)`。
- `(a, b, c)` 创建 Python tuple，可以类比 Java 的小型不可变值对象。
- `f"{...}"` 是 Python f-string，类似 Java 字符串拼接或 `String.format(...)`。

接近的 Java 写法：

```java
record Coord(int row, int col, int layer) {}

String[] startParts = rawTask.getStartNode().getData().get(0).split("_");

Coord startCoord = new Coord(
    Integer.parseInt(startParts[0]),
    Integer.parseInt(startParts[1]),
    Integer.parseInt(startParts[2])
);

String targetLoc = startCoord.row() + "_" + startCoord.col() + "_" + startCoord.layer();
```

需要注意：Python tuple 用下标访问，比如 `start_coord[0]`；Java record 更推荐用有名字的访问器，比如 `startCoord.row()`。

## 安装

### OpenAI Codex CLI

Codex 使用 Agent Skills 标准。你可以让 Codex 从 GitHub 安装：

```text
安装这个 skill：https://github.com/<owner>/<repo>/tree/main/skills/javaboy
```

也可以手动安装：

```bash
mkdir -p ~/.codex/skills/javaboy
curl -o ~/.codex/skills/javaboy/SKILL.md \
  https://raw.githubusercontent.com/<owner>/<repo>/main/skills/javaboy/SKILL.md
```

Windows PowerShell：

```powershell
New-Item -ItemType Directory -Force $env:USERPROFILE\.codex\skills\javaboy
Invoke-WebRequest `
  -Uri https://raw.githubusercontent.com/<owner>/<repo>/main/skills/javaboy/SKILL.md `
  -OutFile $env:USERPROFILE\.codex\skills\javaboy\SKILL.md
```

安装后，开启新一轮 Codex 对话即可使用。

### 项目级安装

如果只想让当前项目使用 Javaboy：

```bash
mkdir -p .agents/skills/javaboy
curl -o .agents/skills/javaboy/SKILL.md \
  https://raw.githubusercontent.com/<owner>/<repo>/main/skills/javaboy/SKILL.md
```

## 推荐仓库结构

```text
your-repo/
  README.zh-CN.md
  skills/
    javaboy/
      SKILL.md
      references/
      scripts/
```

`SKILL.md` 必须直接放在 skill 目录根部：

```text
skills/javaboy/SKILL.md
```

不要多套一层目录，否则安装后可能无法识别。

## 搭配使用

| 搭配方式 | 用途 |
|----------|------|
| `superpowers:systematic-debugging` | 遇到跨语言 bug 时，先系统定位，再用 Java 视角解释根因 |
| `superpowers:test-driven-development` | 修改非 Java 代码前，先补测试，再实现 |
| `superpowers:verification-before-completion` | 防止只解释不验证，适合代码迁移或修复任务 |

## FAQ / 常见问题

### Javaboy 会把所有语言都强行翻译成 Java 吗？

不会。它会先尊重源语言语义，再给 Java 类比。如果 Java 没有等价概念，它会明确说明没有完全等价物。

### 它适合 Java 新手吗？

适合有 Java 基础、正在阅读其他语言代码的人。如果你熟悉 Spring、DTO、service、repository、record、Stream、异常处理等概念，收益会更明显。

### 它能帮我重构非 Java 代码吗？

可以辅助理解和提出建议，但不会强行把 Java 模式搬到其他语言里。比如 Python 里不一定需要写一堆 class，JavaScript 里也不一定需要照搬 Spring 分层。

### 它支持哪些语言？

重点覆盖 Python、JavaScript、TypeScript、Go、Rust、Shell、SQL、YAML、TOML、JSON 配置，以及常见构建和脚本文件。

### 为什么不是直接问“解释这段代码”？

普通解释通常只讲“它做了什么”。Javaboy 额外补上“Java 开发者该如何迁移理解”，并提醒语义差异，减少跨语言误读。

## License

MIT

## Credits

Javaboy 面向 Java 开发者的跨语言代码阅读陪练：先尊重源语言，再建立 Java 心智模型。
