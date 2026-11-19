# Reference-First Restyle · 先参照，后代码

给 AI 编码代理用的一个 Skill：改界面之前，强制走「参照 → 规格 → 候选 → 实现 → 验收」的顺序。

它治的是一个常见病：AI 写的界面能用，但丑。多数时候不是模型不行，是你没给它参照——「高级一点」「现代一点」「有设计感」这类词在模型那里约等于什么都没说，没有参照时它只能回你训练数据的平均值：灰底、蓝按钮、8px 圆角、糊成一团的卡片阴影。

## 它管什么、不管什么

它是一套**流程纪律**，不是审美规则：

- 不负责告诉你什么是好看的（那是 taste 类 skill 的事）；
- 负责保证：没有参照不许动手，没有可执行规格不许写形容词，没有候选方向不许写代码。

和 taste skill 互补：taste 定标准，这个定顺序。单独用也成立——有参照，就有下限。

## 流程

1. **找参照（0 参照不动手）** 用户给的截图/链接最高优先；组件库页面 URL 加 `.md` 常能拿到 AI 可读的结构化 Markdown；项目自己的既有模式也是参照库。
2. **蒸馏成规格，不是形容词** 布局/间距/字阶/圆角/阴影/动效/状态，每条必须能落到具体 CSS。规格里出现「高级感」即为不合格。
3. **候选先行** 一次给 2-3 个方向，说清各自改了什么、差在哪、风险在哪；人选完才写代码。AI 最大的浪费不是写得慢，而是写完一版你不敢用。
4. **三约束实现** 数据结构与 props 不动；不引入新依赖；出完整文件不给 diff。外部参照只取设计、不取代码，按项目自己的技术栈重写。
5. **验收** 构建通过只是及格线。「看起来没问题」不是没问题。

## 安装

把 `SKILL.md` 放进代理的技能目录即可，单文件、无依赖：

```bash
# 项目级（仅当前项目生效）
mkdir -p .agents/skills/reference-first-restyle
curl -fsSL -o .agents/skills/reference-first-restyle/SKILL.md \
  https://raw.githubusercontent.com/Wotrix/reference-first-restyle/main/SKILL.md
```

全局安装则放到 `~/.agents/skills/reference-first-restyle/`。适用于支持 skills 机制的编码代理（ZCode、Claude Code 等）。

## 使用

正常说人话，描述里的触发词会自动匹配：

- 「这个页面太丑了，改观感」→ 会先找参照、给候选，而不是直接动手
- 「照着这张参考图重做这个面板」
- 也可以显式调用 `/reference-first-restyle`

## License

[MIT](LICENSE)
