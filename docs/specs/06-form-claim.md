# Form · 表单理赔申请

画板：https://www.figma.com/design/NiXwro23h7CvvWT7GOb1ep/?node-id=213-24581

全部 Auto Layout；变体用 `状态=`。

## 组件

| 组件 | 属性 |
|---|---|
| 选择器/表单行/就诊医院 | 状态=空态 · 回填-一个 · 回填-多个 |
| 选择器/表单行/事故类型 | 状态=疾病 · 意外 |
| 选择器/选项组 | — |
| 选择器/表单行/就诊时间 | 状态=空态 · 回填 |

## 就诊医院行

- 结构：`LabelSlot`（高 62，与首行对齐）· `Value`（Fill）· `ChevronSlot`（14×62，箭头垂直居中于首行）
- 医院 Tag：横向 Auto Layout（Hug），文案 + 关闭图标；院名长短变化时宽度自适应，过长截断
- 回填-多个：Tags 纵向 Auto Layout，右对齐；箭头只与第一行标签对齐，不随多行整体居中
