# Foundation: Type and color

第一块视觉规则。版式对齐超级助理 SDK「字体」页（示例 / 字号 / 字色 / 场景），**数值走支付宝 APP 基础库 750**，场景写理赔报案与向导。

Figma：https://www.figma.com/design/NiXwro23h7CvvWT7GOb1ep/?node-id=65-16  
页面：`---视觉规范---`（`20:1012`）· 画板 `字体与颜色`（`65:16`）

不要用如流那套 20/16/14/13/12 或品牌蓝 `#4957F2`。那是参考页的栏目结构，不是理赔 token。

## 色块说明

理赔文件没导入 Base collection，APP 语义色 alias 到 Base 时会断链显示成黑。所以规范页色块和示例文字用 **explicit 真实色值**，旁边标 APP token 名——视觉一定对得上，token 名也清楚。生产组件仍应绑 APP 变量。

## Type（PingFang SC）

| 样式 | 750 字号 / 行高 | 字重 | 默认字色 | 理赔场景 |
|---|---|---|---|---|
| Display | 48 / 72 | Medium | TextPrimary · Black 80% | 结果页氛围大标题，少用 |
| Status Title | 40 / 60 | Medium | TextPrimary · Black 80% | 审核中 / 已结案 / 提交完成主标题 |
| Title L | 36 / 56 | Medium | TextPrimary · Black 80% | 页面标题、弹窗标题、主按钮、确认强调字段 |
| Title M | 32 / 48 | Medium | TextPrimary · Black 80% | 一级模块卡：材料清单、信息确认分组 |
| Title S | 28 / 42 | Medium | TextPrimary · Black 80% | 二级标题、列表主文案（医院、材料名） |
| Body L | 30 / 45 | Regular | TextPrimary · Black 80% | 协议长文。常规向导不用 |
| Body M | 28 / 42 | Regular | TextPrimary · Black 80% | 正文、表单值、向导说明 |
| Body S / Caption | 24 / 36 | Regular | TextSecondary · Black 60% | 列表次行、时间、辅助说明 |
| Tag | 20 / 30 | Regular | TextTertiary · Black 40% | 标签、状态小字 |
| Number | 36 / 54 | Medium · Alibaba Sans 102 Ver2 | Price · #FF1A3C | 赔付金额。中文不用此字体 |

字重只有 Medium 和 Regular 两种。代码 / 375：Figma 值 ÷2。Body M 28 → 14。

## Color

| Token | 色值 | 何时用 |
|---|---|---|
| Color/Brand | `#1677FF` | 品牌识别、页面强调色 |
| Color/Button | `#1677FF` | 主按钮底色。与 Brand 同值，语义单列 |
| Color/Link | `#1677FF` | 文字链、PageFooter 可点击字色 |
| Color/TextPrimary | Black 80% | 标题、正文、确认字段 |
| Color/TextSecondary | Black 60% | 次级说明，少用 |
| Color/TextTertiary | Black 40% | 提示、元数据、列表次文案 |
| Color/TextQuaternary | Black 20% | 更弱层级，极少 |
| Color/TextDisable | Black 10% | 输入占位、禁用 |
| Color/Divider | Black 6% | 分割线、细描边 |
| Color/PageBG | `#F0F3F7` | 页面背景（LightBlue 1） |
| Color/CardBG | `#FFFFFF` | 一级卡片、弹窗卡、底栏白底 |
| Color/InnerCardBG | `#F9FAFC` | 卡内嵌套分组、输入区底（LightBlue 2） |
| Color/Alert | `#FF1A3C` | 拒赔、警告短文案。不要整页铺红 |
| Color/Price | `#FF1A3C` | 赔付金额。与 Alert 同值，语义单列 |
| Color/Discount · Notice | `#FF5E1A` | 待补齐、需处理提示 |
| Color/StateFail | `#FF1A3C` | 失败状态图标 / 短结论 |
| Color/StateProcess | `#1677FF` | 审核中 / 处理中图标 |
| Color/StateNotice | `#FF5E1A` | 提醒状态图标 / 短结论 |
| Color/StateSuccess | `#00B865` | 已赔付 / 提交成功。不要大面积装饰绿 |
| Color/FunctionalOverlay | Black 60% | 产品弹窗遮罩 |
| Color/CampaignOverlay | Black 75% | 营销弹窗遮罩。产品确认不要用 |

`#1677FF`（申请按钮）和 `#40B0F8`（查查 Tag）是两套蓝，不要混用。

## 下一步

Selector（列表选择、医院/材料）、信息确认卡、Icon。仍用基础库实例，不手绘。
