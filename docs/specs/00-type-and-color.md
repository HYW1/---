# Foundation: Type and color

第一块视觉规则。版式对齐超级助理 SDK「字体」页（示例 / 字号 / 字色 / 场景），**数值走支付宝 APP 基础库 750**，场景写理赔报案与向导。

Figma：https://www.figma.com/design/NiXwro23h7CvvWT7GOb1ep/?node-id=65-16  
页面：`---视觉规范---`（`20:1012`）· 画板 `字体与颜色`（`65:16`）

不要用如流那套 20/16/14/13/12 或品牌蓝 `#4957F2`。那是参考页的栏目结构，不是理赔 token。

## Type（PingFang SC）

| 样式 | 750 字号 / 行高 | 字重 | 默认字色 | 理赔场景 |
|---|---|---|---|---|
| Display | 48 / 72 | Medium | TextPrimary | 结果页氛围大标题，少用 |
| Status Title | 40 / 60 | Medium | TextPrimary | 审核中 / 已结案 / 提交完成主标题 |
| Title L | 36 / 56 | Medium | TextPrimary | 页面标题、弹窗标题、主按钮、确认强调字段 |
| Title M | 32 / 48 | Medium | TextPrimary | 一级模块卡：材料清单、信息确认分组 |
| Title S | 28 / 42 | Medium | TextPrimary | 二级标题、列表主文案（医院、材料名） |
| Body L | 30 / 45 | Regular | TextPrimary | 协议长文。常规向导不用 |
| Body M | 28 / 42 | Regular | TextPrimary | 正文、表单值、向导说明 |
| Body S / Caption | 24 / 36 | Regular | TextSecondary | 列表次行、时间、辅助说明 |
| Tag | 20 / 30 | Regular | TextTertiary | 标签、状态小字 |
| Number | 36 / 54 | Medium · Alibaba Sans 102 Ver2 | Price | 赔付金额。中文不用此字体 |

代码 / 375：Figma 值 ÷2。Body M 28 → 14。

## Color

| Token | 值 | 何时用 |
|---|---|---|
| Brand / Button / Link | `#1677FF` | 品牌、主按钮、文字链。不要另造第二套蓝；不要和查查 `#40B0F8` 混用 |
| TextPrimary | Black 80% | 标题、正文、确认字段 |
| TextSecondary | Black 60% | 次级说明，少用 |
| TextTertiary | Black 40% | 提示、元数据、列表次文案 |
| TextQuaternary | Black 20% | 更弱层级，极少 |
| TextDisable | Black 10% | 输入占位、禁用 |
| Alert | `#FF1A3C` | 拒赔、警告短文案。不要整页铺红 |
| Price | `#FF1A3C` | 赔付金额 |
| Notice | `#FF5E1A` | 待补齐、需处理 |
| StateSuccess | `#00B865` | 已赔付 / 提交成功的图标或短结论。不要大面积装饰绿 |

## 下一步

Selector（列表选择、医院/材料）、信息确认卡、Icon。仍用基础库实例，不手绘。
