# 自适应：步骤条全家（点 / 标 / 项 / 条 / 列表）

用户说「要自适应」时，**步骤条里每一个组件**都要能随容器宽度和文案重排，不是只改最外层的条。默认宽仍用原稿（常见 750 / 638 / 702）；拉宽实例后必须铺开，右边不许空一截。

## 分层怎么做

| 层 | 组件例 | 怎么自适应 | 不要 |
|---|---|---|---|
| 点 / 标 | AppStepDot、TimelineDot、TimelineBadge | 图形 **固定 px**（48 圆不要拉成椭圆）；标 **HUG** 文字 | 用 `resize()` 把 60 圆拉成 85 |
| 项 | AppStepItem、TimelineItem、ProgressDot、ProcessStepItem、GuideStepItem | 宽 **HUG** 标题/序号；竖向 AL，点在上字在下 | 标题框写死 144，改文案被裁 |
| 列表项 | NoticeItem | 宽 **FILL**；说明文本 FILL | 说明写死 564，列表拉宽字不跟 |
| 条 | AppStepper、TimelineStepper、ProgressStepper、ProcessStepper、GuideStepper | `[项 HUG][间距 FILL + 连线或三角][项 HUG]…` | 间距写成 69/45 的 FIXED Frame |
| 列表 | NoticeList | 项 FILL，纵向上 HUG | 整列写死宽且子项 FIXED |

## 连线

- 步间连线、虚线、三角：**放进 FILL 间距里**，水平 FILL、垂直对齐到点/胶囊中心。
- 项比圆宽时：间距里一段接到项边，**项上左右 stub**（点下面）接到圆的可见边。禁止把线负 x 探进上一列——后画的间距会盖住内圆，像穿过圆心。
- 样式跟原稿 dump：0 高 LINE + `strokeWeight` + `strokeCap`（常见 `SQUARE`），不要用填色矩形冒充描边。
- 底渐变 Absolute，`constraints.horizontal = STRETCH`。
- 徽章、可修改气泡：仍 Absolute + `MIN/MIN`，不要跟着拉变形。
- 不要为连线单独做 COMPONENT。细则：[stepper-bar-lessons.md](stepper-bar-lessons.md)。

## 验收

把任意一条从原稿宽拉到 **900**：

1. 每一步都还在，列距变大，右边不空。
2. 连线/三角跟着间距变长或保持居中，不留在原 x。
3. 改某一项 TEXT，项变宽，间距自动让。
4. 圆点直径不变。

## 和「量原稿」的关系

默认尺寸、线宽、虚线 dash、圆直径仍按原稿 dump。自适应改的是 **谁 FILL / 谁 HUG**，不是把 48 圆估成 50。
