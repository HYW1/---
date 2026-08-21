# Component: Button

理赔申请链路的操作按钮。Figma 规范页用**已发布 APP 基础库**的 Auto Layout 实例，不再手绘胶囊。

对照：`alipay-app-design-system`、盘点 `docs/phase-01-asset-inventory.md` MR-01。

Figma：https://www.figma.com/design/NiXwro23h7CvvWT7GOb1ep/?node-id=62-14  
页面：`Button / 组件`（`56:11`）· 画板 `Button 规范`（`62:14`）

## Assumptions / constraints

- 平台：支付宝 App 内理赔（医疗险）。车险不在本切片。
- Figma 画布 **750**。不要 ÷2。÷2 只用于代码 / 375 逻辑宽。
- 组件真源：已发布团队库「信用卡基础组件」里的 `操作/按钮 Button`（APP token，与基础精简 Copy 同构）。Copy 文件 `4Q2KGg9fstrN2BWCwYChzi` **未发布**，其 key 无法跨文件导入。
- 不要用手绘 Rectangle 冒充 Button；不要把查查 Tag `#40B0F8` 当成按钮蓝。
- Sketch「信息填写」成对按钮 339×98 @2x = 库 ButtonGroup 横向两个里的单颗 L。旧表 169.5×49 pt 是 375 逻辑宽，不是 Figma 尺寸。

## Purpose

- **When to use**：申请表单吸底主操作、成对「暂存 + 提交」、需要文字链取消时。
- **When not to use**：
  - StatusBar / 返回：走基础库，不重做。
  - 药品/医院查查蓝 Tag（`#40B0F8`）：不是 Button。
  - 画布上的 `操作/按钮 Button` 标注条：不是产品按钮。
  - 「一键导入」描边小胶囊：理赔业务扩展，**不是** APP Button 变体。

## 形态 → 库组件

| 理赔用法 | 用这个 | 750 尺寸 | 文案示例 |
|---|---|---|---|
| 单主行动 | Button `尺寸=L` `类型=主按钮` | 718×98 | 提交申请 |
| 成对吸底 | ButtonGroup `类型=横向两个` | 742×146（内两颗 339×98） | 暂存 / 提交申请 |
| 取消申请 | PageFooter `文字可点击` `单入口` | 750×116 | 取消申请 |
| 不可用 | Button `状态=不可用` | 同尺寸 | 提交申请 |
| 警告 | Button `类型=警告` | L 718×98 | 放弃 |

库还有 XS/S/M/XL 与次按钮，申请吸底默认用 L。S/M 随文案 hug：默认「行动文案」时 S `172×60`、M `192×80`（Copy 文件里同变体曾是 176 宽）。

## Published import keys

| Asset | Key |
|---|---|
| Button | `6da3c2344daa541d3323897a609ef2161b943234` |
| ButtonGroup | `0ae9085c2ede5c93c3588c19ea0b6c6d9dd439e5` |
| PageFooter | `20e518c6636ea3b981f6245182cd22fe3df5859c` |

文本属性：`按钮文案`。主色 `Color/Button` `#1677FF`。字：PingFang SC Medium 36 @750（L）。

## Sketch 历史值（375 / 代码，不要画进 Figma）

图层：`按钮/蓝色/可操作`。2x 画布 ÷2 = pt。

| 项 | 2x | 1x pt | 说明 |
|---|---|---|---|
| 成对单颗 | 339×98 | 169.5×49 | 对应库 ButtonGroup 内 L |
| Outline「一键导入」 | 192×49，圆角 8 | 96×24.5 | 业务扩展，未入库 Button |
| 文字「取消申请」 | 字号 26 / `#1677FF` | 13pt | 现用 PageFooter，不再手写文字链 |

## 不要做

- 手摆两颗胶囊冒充 ButtonGroup
- 把「取消申请」做成第三颗胶囊或 Button Text 变体（库没有 Text 类型）
- 把 Pressed / Loading 从截图估出来（库有「不可用」，用那个）
- 在 Figma 里把 718×98 ÷2

## 下一张切片

Selector（申请表单行：Label + Value + Chevron）。优先导入基础库 ListItem / InputListItem。
