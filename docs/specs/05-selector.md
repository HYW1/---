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

## 4. 选择面板

### 4.1 就诊医院 HospitalSelector

| 组件 | 属性 |
|---|---|
| 选择器/就诊医院 HospitalSelector | 状态=默认 · 添加后 · 搜索结果 |

元件：SheetHeader · SearchBar · SectionTitle · GradeBadge · HospitalItem · HospitalPill · SelectedChip · SelectControl

### 4.2 查查（医院查查 / 药品查查）

历史稿 Sketch 导入后结构混乱，已按截图重做 Auto Layout。

**元件**

| 组件 | 属性 |
|---|---|
| 选择器/查查搜索栏 LookupSearchBar | — |
| 选择器/筛选触发 FilterTrigger | 状态=默认 · 展开（箭头↓/↑，展开蓝色） |
| 选择器/筛选胶囊 FilterPill | 状态=默认 · 展开 |
| 选择器/查查标签 LookupTag | 状态=选中 · 未选 |
| 选择器/级联侧栏项 CascadeSideItem | 状态=默认 · 选中（左侧蓝条） |
| 选择器/级联列表项 CascadeListItem | 状态=默认 · 选中（蓝色文案） |

**面板**

| 组件 | 属性 | 结构 |
|---|---|---|
| 选择器/药品查查 MedicineLookup | 状态=疾病面板 | 搜索栏 + 筛选触发行 + 标签网格（3 列） |
| 选择器/医院查查 HospitalLookup | 状态=城市级联 | 搜索栏 + 筛选胶囊行 + 省市级联（侧栏+列表） |

## 5. 确认条 ConfirmBar

面板底部操作，随已选数量切换可点态。

| 组件 | 属性 |
|---|---|
| 选择器/就诊医院/确认条 ConfirmBar | 状态=不可点 · 可点-单个医院 · 可点-多个医院 |
