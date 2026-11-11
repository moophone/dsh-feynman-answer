# dsh-feynman-answer

把「费曼五段式」作为解释型回答的默认骨架。一个 DSH 插件包，只发一个技能，不注入任何 loader 行。

Makes the five-part Feynman-style answer the default shape for explanatory replies in
DeepSeek Harness. A DSH bundle that ships one skill and injects nothing into any profile.

## 它做什么 / What it does

技能会在「讲清楚一件事」的目标下套用五段骨架，标题逐字照抄、顺序不变：

```
## 1.先说结论

## 2.相应论点核心内容（前有序号）

## 3.总结

## 4.启示及未来行动指南

## 5.奥卡姆剃刀总结
```

**什么时候用**：讲清一个概念、解释一个原因、比较两个方案、说明一段代码为什么这样写、复盘一次故障、给出一个判断并交代理由。

**什么时候不用**：一行确认、状态回执、报错原文转述；纯执行报告（改了哪些文件、跑了什么命令）；用户只要一个数字或一段代码；用户明确要求别的格式。

判断标准只有一句：**删掉五段骨架后信息有损失吗？没有就不用。**

## 安装 / Install

```bash
dsh plugin --profile desktop add dsh-feynman-answer
```

从 GitHub 安装：

```bash
dsh plugin --profile desktop add "git+https://github.com/moophone/dsh-feynman-answer.git#main"
```

重启 DSH 后，技能出现在技能目录里。

## 让五段式成为默认习惯 / Making it the default

技能负责「怎么按五段式答」，但不会自动让 AI 每轮都想起它。装好后对 AI 说一次：

> 请记住：以后凡是解释型、教学型、阶段汇报、收尾总结、给判断并交代理由的回答，
> 都按费曼五段式作答（1.先说结论 / 2.相应论点核心内容（前有序号） / 3.总结 /
> 4.启示及未来行动指南 / 5.奥卡姆剃刀总结），标题逐字照抄、顺序不变。
> 只有纯执行回执、一行确认、只要一个数字或代码片段时不套用。

这句话会被存进 runtime memory，之后每轮对话都生效。

## 改格式 / Changing the format

只改 `skills/feynman-answer/SKILL.md`。五个标题在正文的代码块里，逐字照抄即可。

## 为什么不注入 profile / Why nothing is injected

DSH 的 profile 补丁里没有能注入全局回复指令的配置位，所以这个插件的 `patch` 是空的
——`cordis.patch.yml` 只有注释。这样它不会碰用户 profile 里任何手写的 loader 行。

## 文件 / Files

```
dsh-feynman-answer/
├─ package.json              dsh.bundle.patch 指向 cordis.patch.yml（空补丁）
├─ cordis.patch.yml          纯注释，不注入任何 loader 行
├─ skills/feynman-answer/SKILL.md   技能正文（五段骨架 + 走形对照表）
├─ icon.svg                  列表图标
└─ README.md
```

## 许可 / License

MIT
