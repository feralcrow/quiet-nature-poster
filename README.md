# 静谧自然海报 · Quiet Nature Poster

一套「低饱和自然系 + 诗意克制文字」的海报生成规则库，写成 AI Agent 可直接执行的 skill：
给它一个主题、一张参考图、或者只是几个颜色，它回你一套完整方案 —— 诗意标题、四色板（含 hex
与面积占比）、主元素、构图骨架、材质光线、A/B 两版正向提示词、共用负向提示词、排版建议。

核心审美：低饱和自然意象 × 东方日系留白 × 胶片/纸张颗粒 × 诗意但克制的文字。

This is a written visual system, packaged as an agent skill. Feed it a theme, a reference
image, or just a colour, and it returns a full poster plan: poetic title, a four-colour
palette with hex and area ratios, one hero element, a compositional skeleton, material and
light notes, two positive prompts (restrained × expressive) and a shared negative prompt.

## 仓库结构

| 路径 | 内容 | 适合谁 |
|---|---|---|
| `SKILL.md` + `references/` | 完整版：26 组色板、逐条推导依据、参考图案例研究（约 95 KB 规则文本） | 想彻底复刻这套审美、愿意读长文档的人 |
| `lite/` | 轻量版：9 组代表色板 + 完整配色推演表，自包含可独立开工 | 想直接用、或只想先试风格的人 |

两个版本规则一致，完整版只是多了推导过程、案例与更多色板。轻量版是推荐的上架/分发单元。

## 安装

Cola（Skill Hub / find_skill 走 GitHub 源）：

```text
完整版： source = feralcrow/quiet-nature-poster
轻量版： source = feralcrow/quiet-nature-poster , directory_path = lite
```

手动：把 `lite/` 整个目录拷进 `~/.cola/skills/quiet-nature-poster-lite/`（或对应 agent 的 skills 目录）即可，
包内文件互相引用都是相对路径。

## 三个典型用法

1. **只给主题** —「做一张『凌晨四点，海还没醒』的竖版海报」
   → 自动选板（海风灰蓝系）、定主元素（海平线）、低位地平线骨架，出 A/B 两版提示词。
2. **只给颜色** —「就用 `#6E8CA8` 这个蓝做张海报」
   → 进入色板驱动模式：把这颗种子推成四色板（含明度阶梯与面积占比），反查出色相→主题方向，
   直接出方案，并回显你的原色被改了什么。**说「别改」它就一字不动地锁定，改的是其余三色和材质。**
3. **给参考图** —「按这张图的画风做系列」
   → 先区分「稳定风格」与「图专属母题」，只把前者吸收成规则，再按系列化流程出核心版 + 2 个变体。

## 推荐提示语

```text
做一张「凌晨四点，海还没醒」的竖版海报，安静自然风格，不要叠任何模式。
```

```text
就用 #6E8CA8 这个蓝做张海报，别改这个颜色，其余配色你自己推。
```

```text
按这张参考图的画风出一套三张的节气系列，固定配色与材质，只换主元素，标题要一版克制一版飞扬。
```

## 几条值得先知道的硬规则

- 强调色面积 3%–8%，超了就俗；主元素永远只有一个。
- 不要求模型生成可读中文：图像模型的中文不可靠，且字体授权无法证明。提示词只描述字体气质，
  正式发布用已确认授权的开源字体后期重排。
- 用户给的强制文字逐字保留，连标点和换行都不改 —— 与「这个颜色别改」同级。
- 出图后颜色被模型拉艳是最常见失败，包里附了二次收敛短语。

## 版本与变更

见 [CHANGELOG.md](CHANGELOG.md)。当前 `0.2.0`（2026-08-29）：新增色板驱动模式，拆出 `lite/` 分发包，
补上许可声明。

## 授权

规则库文档本身：**CC BY-NC 4.0**（署名 · 非商业使用），见 [LICENSE](LICENSE)。

**你产出的海报、提示词、配色方案不受此限制** —— 拿去接商单、印刷、发布都可以，不需要署名。
被约束的是这些文档本身的再分发与打包转售。想要商业授权请开 issue。
