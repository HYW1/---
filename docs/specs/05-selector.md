# Selector · 选择器

画板：https://www.figma.com/design/NiXwro23h7CvvWT7GOb1ep/?node-id=213-23970

按选择器规范分层：**选项标签 → 选项组 → 表单行 → 选择面板 → 确认条**。

## 1. 选项标签 FilterChip

原子选项，供选项组 / 行内选择复用。

| 组件 | 属性 |
|---|---|
| 选择器/选项 | 状态=选中 · 未选 |

## 2. 选项组 OptionGroup

选项标签的行列编排。

| 组件 | 属性 |
|---|---|
| 选择/选项组 OptionGroup | 行数 · 列数 · 选项样式（一行字 / 两行字） |

## 3. 表单行 FormRow（触发器）

进入选择的入口，分跳转型与行内型。

| 组件 | 类型 | 属性 |
|---|---|---|
| 选择器/表单行/就诊医院 | 跳转选择 | 状态=空态 · 回填-一个 · 回填-多个 |
| 选择器/表单行/就诊时间 | 跳转选择 | 状态=空态 · 回填 |
| 选择器/表单行/事故类型 | 行内选择 | 状态=疾病 · 意外 |

- 跳转选择：右侧文案/标签 + 箭头，打开选择面板
- 行内选择：右侧直接放选项组，无需弹层

## 4. 选择面板 HospitalSelector

弹层主体（搜索 / 历史 / 热搜 / 列表）。

| 组件 | 属性 |
|---|---|
| 选择器/就诊医院 HospitalSelector | 状态=默认 · 添加后 · 搜索结果 |

元件：SheetHeader · SearchBar · SectionTitle · GradeBadge · HospitalItem · HospitalPill · SelectedChip · SelectControl

## 5. 确认条 ConfirmBar

面板底部操作，随已选数量切换可点态。

| 组件 | 属性 |
|---|---|
| 选择器/就诊医院/确认条 ConfirmBar | 状态=不可点 · 可点-单个医院 · 可点-多个医院 |
