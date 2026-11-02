# article-brief

把一篇文章压成一份**固定结构的简报**：结论 → 骨架 → 逐节要点 → 证据 → 立场 → 存疑。

不是"帮我总结一下"那种复述目录的摘要。它要求每条要点带锚点（`[§3]`、`[¶12]`），把「作者主张 / 支撑证据 / 我的判断」分开写，并在正文没读全时明说缺了什么。

## 为什么需要它

大多数文章摘要失败在三个地方：

1. **按小标题顺序复述**——读完仍不知道作者在论证什么；
2. **把作者的断言当结论**——简报失去了"值不值得信"的判断；
3. **没读全却装作读全了**——后半段凭空补全。

这个 skill 用一份输出契约把这三个坑堵上：三档固定模板、锚点约定、证据分型、"截断必声明"。

## 三种档位

| 档位 | 上限 | 用在什么时候 |
| --- | --- | --- |
| `one-line` | 1 句 ≤ 60 字 | 先判断值不值得读 |
| `five-min` | 中文 ≤ 700 字 | 默认 |
| `outline` | 中文 ≤ 2000 字 | 要逐节结构、论证链、可执行项 |

## 产出长什么样

真实示例见 [`examples/worked-example.md`](examples/worked-example.md)，节选：

> **结论**：作者认为 Agent 生态的竞争已从"模型更强"转向"给 Agent 装什么样的手艺"，而本周周榜 13/16 个项目是 Coding Agent Skill 这一事实就是证据。
>
> **关键证据**
>
> | 主张 | 证据 | 类型 | 可核性 |
> | --- | --- | --- | --- |
> | C1 竞争重心转向"手艺" | 16 个项目里 13 个服务于 Agent | 数据（星数排序） | 可核，但星数≠采用率 |
>
> **存疑之处**
> - C1 是从星数推出来的，而文章自己承认日榜容易被单条社交媒体带起——周榜也有同样问题，只是弱一些。

## 安装

Skill 就是一个文件夹，核心是 `SKILL.md`。

**DeepSeek Harness**

```bash
git clone https://github.com/xingguiji/article-brief.git ~/.dsh/skills/article-brief
```

**Claude Code**

```bash
git clone https://github.com/xingguiji/article-brief.git ~/.claude/skills/article-brief
```

**其它宿主**（Codex / OpenCode / 各类自建 agent）：把整个目录放进该宿主的 skills 目录即可，`SKILL.md` 的 frontmatter 会被读取；正文里对抓取工具的称呼按宿主替换（DSH 是 `web_fetch`，Claude Code 是 `WebFetch`）。

## 用法

直接用自然语言触发，不需要记命令：

- 「总结这篇文章 https://…」
- 「这篇讲什么，值不值得读」→ 走 `one-line`
- 「把它的结构梳理出来，逐节」→ 走 `outline`
- 「这文章的论证站得住吗」→ 走 `five-min`，重点看「关键证据」和「存疑之处」
- 也可以直接给本地文件、粘贴的全文、PDF、访谈转录

## 目录

```
SKILL.md                         入口：什么时候用、四遍读法、硬性规则
references/output-contract.md    三档模板、锚点约定、禁止句式
references/extraction.md         截断、付费墙、超长文、非文本输入的降级策略
examples/worked-example.md       一篇真实文章的完整简报 + 同篇的 one-line 版
```

## 设计原则

- **锚点即诚实**：无法定位到原文的要点，不写。
- **评价换事实**："结构清晰、论证严密"这类句子一律删除，换成原文里那一句。
- **不编数字**：原文没有的机构、日期、百分比，一个都不补。
- **半份简报好过一份虚构的完整简报**。

## English

`article-brief` turns an article into a fixed-section brief: thesis, skeleton, per-section points, the evidence behind each claim, the author's implicit assumptions, and what does not hold up. Every point carries an anchor (`[§3]`, `[¶12]`), author claims are separated from evidence and from the agent's own judgment, and a truncated fetch must be declared up front.

Install into `~/.claude/skills/article-brief` or `~/.dsh/skills/article-brief`. Trigger it with "summarize this article", "outline its structure", "is this argument sound", or "is it worth reading".

## License

MIT © 2026 xingguiji
