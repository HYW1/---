# Component: Button

第一份规范切片。只覆盖理赔申请链路里已经量到的按钮，不覆盖 Kitchen 导航返回、不覆盖查查 Tag。

对照盘点：`docs/phase-01-asset-inventory.md` §1.5、MR-01。

## Assumptions / constraints

- 平台：支付宝 App 内理赔（医疗险）。车险不在本切片。
- 主视觉：申请步骤 1–3 截图 = 当前页面层级；**尺寸以本地 Sketch「信息填写」原生图层为准**。
- Sketch 画布按 2x 记录。表内同时给 2x 与 1x pt。
- 未见的状态不写建议值。
- Token 名是占位，仓库里还没有已发布 Variable。HEX / 字号先挂在 L1 值上，不假装已经有 Token 表。
- 本切片 **不创建 Figma Component**。

## Purpose

- **What it is**：理赔业务自己的操作按钮（提交、暂存、取消、材料卡上的线框动作）。
- **When to use**：申请表单吸底主操作、材料卡次要动作、需要文字链取消时。
- **When not to use**：
  - StatusBar / 返回：走 Kitchen，不重做。
  - 药品/医院查查的蓝 Tag（`#40B0F8`）：不是 Button。
  - 画布上的 `操作/按钮 Button` 标注条：不是产品按钮。

## 先分清三套形态（不要合成一个 Component Set）

| 形态 | 场景 | Evidence | 本切片 |
| --- | --- | --- | --- |
| **成对胶囊** 暂存 + 提交申请 | Sketch 信息填写吸底 | L1 Exact | 主规格 |
| **全宽胶囊** 「提交信息」 | 最新流程申请步骤截图 | L3 只认形态 | 记下冲突，不写高度 |
| **线框小胶囊** 「一键导入」/ Symbol「主要操作」 | Sketch 材料卡 | L1 Exact | 次规格，尺寸独立 |
| **文字按钮** 「取消申请」 | Sketch 吸底组合上方 | L1 Exact（字号/色） | 次规格 |
| **弹窗主按钮** 「我知道了」「选它」 | 门户 / 方式选择 / 预审截图 | L2/L3 | 只记用途，尺寸未量 |

最新流程截图里主按钮经常是**一条全宽胶囊**，Sketch 里是**左右各半**。两条都真实存在。冲突时：**成对规格用 Sketch L1；全宽只承认“有这种布局”，高度不从截图估。**

## Anatomy

成对 / 全宽主按钮：

1. Container（胶囊底或白底描边）
2. Label（单行）

文字按钮：只有 Label，无底、无描边。

线框小胶囊：Container 描边 + Label。

**Content rules（已见到的）**

- Label 均为单行中文，PingFang SC Regular。
- 尚未见到图标按钮、双行文案、超长截断。超长规则 = 未见。

## Variants（已证实）

建议 API 先按「形态」拆，不要用一个 `size` 硬塞：

| Prop | 值 | 含义 | Evidence |
| --- | --- | --- | --- |
| `emphasis` | `primary` | 蓝底白字，主提交 | L1 |
| `emphasis` | `secondary` | 白底灰描边，暂存 | L1 |
| `emphasis` | `text` | 无底，蓝字取消 | L1 |
| `emphasis` | `outline` | 蓝描边小胶囊，材料卡动作 | L1 |
| `layout` | `pair` | 吸底左右各一，宽 339 @2x | L1 |
| `layout` | `fullWidth` | 截图中的全宽主按钮 | L3，无 Exact 宽高 |
| `state` | `enabled` | 目前唯一能量到的 | L1 |

未见，因此 **不进 API**：`loading`、`disabled`、`pressed` 的视觉值、icon、danger。

无效组合：`text` 不与 `pair` 并排当一半胶囊用——「取消申请」在成对按钮**上方**，不是第三颗胶囊。

## Exact 值（L1 Sketch，信息填写吸底）

图层：`按钮/蓝色/可操作`；吸底：`信息输入:50/按钮Button:2/吸底组合/状态:#默认状态`。

| 项 | 2x | 1x pt | 填充 / 描边 | 文字 | Evidence |
| --- | --- | --- | --- | --- | --- |
| Primary 容器 | 339×98，圆角 49 | 169.5×49，胶囊（圆角 = 高/2） | `#1677FF` | 「提交申请」PingFang SC Regular 36 / `#FFFFFF` | L1 |
| Secondary 容器 | 339×98，圆角 49 | 169.5×49 | `#FFFFFF` + 描边 `#E5E5E5` **2px @2x** | 「暂存」PingFang SC Regular 36 / `#333333` | L1 |
| 成对占位 | 两颗宽合计 678；750 − 678 = 72 | 36pt 留给左右边距 + 中间缝 | 缝如何拆分 **未见单独图层** | — | L1 宽可加总；gap 不写成 Exact |
| 吸底组合 | 750×263 | 375×131.5 | 白底 | 内含成对按钮 + 文字取消 | L1 |
| Text「取消申请」 | — | — | 无底 | PingFang SC Regular 26 / `#1677FF` | L1 |
| Outline Symbol | 144×49，圆角 **8** | 72×24.5，圆角 4 | 描边 `#1677FF` 2px @2x | 「主要操作」Regular 24 / `#1677FF` | L1 |
| Outline 实例「一键导入」 | 192×49 | 96×24.5 | 同上结构，宽被拉开 | 同左 | L1 |

注意：Outline Symbol 图层名带「胶囊」，但记录圆角是 **8 @2x**，不是高度一半。和主按钮胶囊不是同一圆角规则。以 JSON 为准，名称不覆盖数值。

## States

| State | UI | Evidence |
| --- | --- | --- |
| Enabled / Default | 上表 | L1 |
| Pressed | 未见 | 不写 |
| Disabled | 未见 | 不写 |
| Loading | 未见 | 不写 |
| Focused | 支付宝 App 内，未见独立焦点稿 | 不写 |

## Layout rules

- 成对主操作固定在申请页**吸底**，不跟表格内容一起滚走（Sketch 吸底组合 750 宽）。
- 文字「取消申请」在成对按钮之上，同色 `#1677FF`，字号小于主按钮（26 vs 36 @2x）。
- 线框小胶囊用在材料卡内部（「一键导入」），不要拉成 339 宽去冒充 Secondary。
- 全宽主按钮（L3）：出现在最新申请步骤截图，作为「只有一颗主操作」时的布局。高度/边距未量。

## Token hooks（占位，未发布）

| 钩子 | 先绑这个值 | 不要绑 |
| --- | --- | --- |
| 主色 / 主按钮底 / 文字按钮字色 | `#1677FF` | `#40B0F8` |
| 主按钮字 | `#FFFFFF` | — |
| Secondary 字 | `#333333` | — |
| Secondary 描边 | `#E5E5E5` | 不要用主色描成对暂存（成对暂存是灰描边，不是蓝描边） |
| Outline 描边与字 | `#1677FF` | 与 Secondary 不是同一套描边 |
| 主按钮字号 | 18pt（36 @2x）Regular | Outline 是 12pt（24 @2x） |
| 文字按钮字号 | 13pt（26 @2x）Regular | 不要和主按钮 18pt 混用 |

字体家族：PingFang SC。数字字体（DINPro / Alibaba Sans）未出现在按钮 Label 上。

## Accessibility

- 每颗按钮的 Name = Label 原文（提交申请 / 暂存 / 取消申请 / 一键导入）。
- 成对点击区域：容器 169.5×49 pt，高于常见 44pt 下限。
- Outline 实例高 24.5 pt，**低于 44pt**。这是材料卡内小动作，不是吸底主操作。是否加热区 = 未见，不编。
- 对比：蓝底白字、白底 `#333333` 字，稿面如此；未做对比度测算。

## 和 Kitchen / 其它库的关系

- Overlay、Toast、StatusBar、返回：**复用 Kitchen**，本组件不管。
- WorldFirst / Antom / 信用卡 / AlipayHK 按钮：**不用**。
- `#1677FF` 在其它库里可能叫 link/brand，理赔按钮仍以本表为准。

## QA checklist

- [x] 成对 Primary / Secondary 有 L1 宽高、圆角、填充、字
- [x] 文字取消与 Outline 小胶囊已分开，不和成对按钮抢同一尺寸
- [x] 全宽截图布局已并列，未把估高写进表
- [ ] Pressed / Disabled / Loading — 未见，不验收
- [ ] 全宽胶囊高度 — 缺可量节点
- [ ] 成对按钮中间缝与左右边距如何拆 72px @2x — 未拆
- [ ] Outline 圆角 8 是否笔误 — 名称像胶囊，数值不像

## Open questions（只问会改 API 的）

1. 最新申请步骤的全宽「提交信息」，是否取代 Sketch 成对「暂存 + 提交申请」，还是两种布局都保留（有暂存用 pair，无暂存用 fullWidth）？
2. Outline 圆角以 JSON 的 8 @2x 为准，还是应按胶囊（高/2）重测？
3. Disabled / Loading 若线上有，请给一帧原生稿（Sketch 或 Figma 可编辑图层），不要截图估色。

## 下一张切片

Selector（申请表单行：Label + Value + Chevron）。仍先写文档，不建 Figma 组件。
