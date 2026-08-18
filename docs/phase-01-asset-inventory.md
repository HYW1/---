# 理赔业务 Design System — Phase 01 资产盘点

> 本阶段只做盘点，不创建规范页、不创建组件、不修改任何现有设计。
> 无法从 Figma 原生结构直接读取的参数一律标为 **Visual Estimate / 待人工确认**，不写成精确 Token。

## 扫描范围

| 文件 | File Key | 页面 | 角色 |
| --- | --- | --- | --- |
| 理赔侧设计规范 | `NiXwro23h7CvvWT7GOb1ep` | `封面` `37:523` | 封面，无业务组件 |
| 理赔侧设计规范 | `NiXwro23h7CvvWT7GOb1ep` | `历史稿` `0:1` | 历史设计 + 部分可编辑稿 |
| 理赔侧设计规范 | `NiXwro23h7CvvWT7GOb1ep` | `理赔业务流程` `19:880` | 最新业务流程稿 |
| skill（Sketch 导入） | `ZXibIc4lflyHRoTF7OQV0L` | `历史稿` `0:1` | **暂停使用**，待你确认 |
| 本地 Sketch（ZIP 解析） | 对话上传 `…250905…sketch` | `页面 1` + `控件` | 信息填写 + 多责任赔付，**原生图层可读** |

此前误把 Figma 文件 `skill`（`ZXibIc4lflyHRoTF7OQV0L`）当作 Sketch 导入；**在你确认前不再使用该文件。**

本地 Sketch **可以换方法读**：把 `.sketch` 当 ZIP 解出 `pages/*.json`，图层尺寸 / 填充 / 字体是 L1 Exact。Figma 授权 **读不到** 你电脑上的 Sketch；本环境是 Cloud Agent，看不到 Mac 磁盘。

范围已确认：

- 申请步骤 1/2/3 截图 = 当前主视觉
- 理赔有两种申请方式：向导协助申请 / 自助申请
- **车险暂不纳入**
- 无法提取的组件接受人工复刻；组件截图见 `docs/phase-01-component-crops/`

## 证据等级

| Level | 含义 | 本阶段用法 |
| --- | --- | --- |
| L1 Exact | Figma Component / Instance / Variable / Style / 可读取图层；**或 Sketch 原生 JSON 图层**（2x 画布需 ÷2 才是 pt） | 可进入后续正式 Token |
| L2 Repeated Pattern | 多个页面重复出现的稳定结构 | 可进入后续正式规范，尺寸仍需复核 |
| L3 Visual Recognition | 图片 / Screenshot / Flattened UI 视觉识别 | **必须人工确认后才能进 Token** |
| L4 Recommendation | 项目中没有明确规范 | 本阶段不给建议值 |

## 关键结论（先看这个）

1. **本项目几乎没有“理赔业务自己的 Figma 组件库”。** 理赔侧文件 published components = 0。现有 Instance 主要来自外部库（导航、遮罩、关闭按钮、标注条），不是理赔表单/上传/选择器。
2. **最新业务流程稿的申请主链路，大部分是整屏截图。** `申请步骤1/2/3`、`选择申请方式`、`签名协议`、`理赔记录` 等都是 named Frame 包一层 `image xx`。视觉上能识别组件，但 **不能假装已经提取成功**。
3. **Figma 里的「Sketch 导入」先停用。** 真正的本地 `.sketch` 要用 ZIP 解析，不要走 Figma 导入（导入后 Symbol 丢失、变整屏图）。
4. **已成功解析的这一份 Sketch 不是全链路。** 只有「信息填写备份 117–129」和「多责任赔付-2条/7条」，外加 1 个线框胶囊按钮 Symbol。门户 / 进度 / 拒赔 / 签名等历史稿仍在你本地其他 Sketch 里，**这份读不到。**
5. **可直接复用的 Figma 原生结构集中在「疾病查查 / 就诊医院」选择器链路。** 这里有 `BottomSheet`、`SearchBar`、`HotSearchPillsGrid`、`SelectionConfirmPanel` 等 named Frame，属于隐性组件，不是 Component Set。
6. **画布上的 `操作/按钮 Button` Instance 多数是流程标注条，不是产品按钮。** 宽 3000–12000px、高 128px。不要把它当成 Primary Button 规范源。
7. **产品按钮的第一份 L1 Exact 来自这份 Sketch，不是 Figma 截图。** 吸底「暂存 / 提交申请」是原生 group `按钮/蓝色/可操作`。

---

## 1. 页面清单 Page Inventory

### 1.1 理赔侧设计规范 / 封面

- `封面`：文件封面「理赔设计规范 / 蚂蚁保 / 2026.06.05」。无组件。

### 1.2 理赔侧设计规范 / 历史稿 `0:1`

可命名的主要屏幕（750 宽移动稿，含重复态）：

| 屏幕 | Node | 来源类型 | 备注 |
| --- | --- | --- | --- |
| 咨询向导长页 `3` | `5:421` | Implicit + Native | 可编辑图层较多 |
| 疾病查查相关 `855/834/838/848/836/844/842/839/856/841/857` | `5:561` 等 | Implicit | 编号页，部分可编辑 |
| 就诊医院 Default / 搜索中 / 添加 / 搜索完 | `5:1280` `5:1740` `5:1970` `5:2375` | Implicit | **选择器核心，可分析结构** |
| 甲状腺癌浮层 ×5 | `5:3098` 等 | Implicit | 疾病说明 Bottom Sheet |
| 疾病查查 | `5:4303` `5:4411` | Mixed | |
| 有安心赔 / 无安心赔 | `8:5361` 等 | Mixed | 门户差异态 |
| 医院查查 / 信息填写备份 / 第二步-意外 / 电票优化 | 多个备份 Frame | Implicit / Page-specific | 历史迭代稿 |
| 大量 `image 37/39/161–215` | 见第 4 节 | Image / Screenshot | 无法读内部图层 |

### 1.3 理赔侧设计规范 / 理赔业务流程 `19:880`

这是最新流程。**优先级高于历史稿。**

| 屏幕 | Node | 来源类型 | 是否整屏图片 |
| --- | --- | --- | --- |
| 我的-理赔入口 | `20:1214` `22:3836` | Implicit（大量 Vector/Mask） | 否，但图层高度 flatten |
| 理赔门户 | `20:1556` `22:3642` | Implicit | 否，图层可部分读取 |
| 首次弹窗 | `20:1743` | Implicit Dialog | 否 |
| 咨询向导 | `20:2077` | Mixed | 待复核 |
| 医院查查 | `20:2290` | Implicit | 否 |
| 安心赔说明页 | `20:2497` | Implicit | 否 |
| 互动式理赔 | `22:3631` | Image | 是 `image 12` |
| 保单详情 | `22:2997` | Image | 是 `image 13` |
| 选择申请方式 | `22:2998` | Image | 是 `image 14` |
| 申请步骤1 | `22:2999` | Image | 是 `image 15` |
| 申请步骤2-疾病 | `22:3008` | Image | 是 `image 16` |
| 申请步骤2-意外 | `22:3012` | Image | 是 `image 17` |
| 申请步骤3 ×3 | `22:3022/3024/3025` | Image | 是 `image 18/19/20` |
| 签名协议 | `22:3048` | Image | 是 `image 21` |
| 签名 | `22:3049` | Image | 是 `image 22` |
| 理赔预审 | `22:3413` | Mixed / 视觉识别 | 浮层可识别，底层步骤条偏图片 |
| 理赔记录 | `22:3636` `22:4198` | Image | 是 `image 23/25` |
| 运费险记录 | `22:3641` | Image | 是 `image 24` |
| 老带新分享页 / 分享浮层 / 分享到微信 / 分享口令 | `22:4199` 等 | Image | 是 |
| 就诊医院 / 甲状腺癌浮层 / 疾病查查 | 与历史稿重复 | Implicit | 否 |

### 1.4 未确认文件（暂停使用）

Figma `skill`（`ZXibIc4lflyHRoTF7OQV0L`）先不作为理赔历史源。车险相关屏幕先不纳入。下面这张业务地图仍有效，但证据应改从**本地 Sketch ZIP**补，不要从该 Figma 文件读。

### 1.5 本地 Sketch（ZIP 解析）— 已读通一份

读取方式：`.sketch` = ZIP，解出 `document.json` + `pages/*.json`。这比 Figma 导入更准，能拿图层宽高、填充 HEX、字体、圆角。

已读文件：对话上传 `________-____250905_1__3__2dea.sketch`（Sketch 2025.2，约 5.8MB）。预览：`docs/phase-01-component-crops/sketch-preview-info-fill.png`。

**这份覆盖什么**

| 画板（750 宽，2x 画布） | 类型 | 备注 |
| --- | --- | --- |
| `信息填写备份 117–129`（13 个） | Native Group | 上传材料卡 + 吸底按钮 + 不合理费用说明浮层 |
| `多责任赔付-2条` 备份 ×4、`多责任赔付-7条备份 10` | Native Group | 赔付明细，不是申请三步主链路 |
| `控件` 页 Symbol | Native symbolMaster | 仅 1 个：胶囊线框按钮 24px |

**这份不覆盖什么：** 门户、选择申请方式、申请步骤 1/2、签名、理赔记录、拒赔矩阵、进度时间轴。那些还在你本地其他 Sketch 里。

**Sketch L1 Exact（2x 画布；1x pt = 数值 ÷ 2）**

| 组件 | Sketch 图层 | 2x | 1x pt | 填充 / 描边 / 字 | Evidence |
| --- | --- | --- | --- | --- | --- |
| Primary Button | `按钮/蓝色/可操作` + Background | 339×98，圆角 49 | 169.5×49，胶囊 | `#1677FF`；字「提交申请」PingFang SC Regular 36 / `#FFFFFF` | L1 Sketch |
| Secondary Button | 同上，白底 | 339×98，圆角 49 | 169.5×49，胶囊 | `#FFFFFF` + 描边 `#E5E5E5` 2px；字「暂存」PingFang SC Regular 36 / `#333333` | L1 Sketch |
| 吸底组合 | `信息输入:50/按钮Button:2/吸底组合/状态:#默认状态` | 750×263 | 375×131.5 | 白底；含「取消申请」PingFang SC Regular 26 / `#1677FF` | L1 Sketch |
| Outline Capsule | Symbol `胶囊按钮(线框) 24px` | 144×49，圆角 8 | 72×24.5，圆角 4 | 描边 `#1677FF` 2px；字「主要操作」PingFang SC Regular 24 / `#1677FF` | L1 Sketch |
| Outline Capsule 实例 | 信息填写页「一键导入」 | 192×49 | 96×24.5 | 同上结构，宽被拉开 | L1 Sketch |
| 材料卡 | `编组 4备份` 等 | 宽 702 | 351 | 白底；标题 PingFang SC Semibold 32 / `#333333`；「必须提供」；「材料示例」24 / `#1677FF` | L1 Sketch |
| 页面底 | `信息填写备份 117` | 750 宽 | 375 | 页背景 `#F5F5F5` | L1 Sketch |

高频字色（这份 Sketch 文本直方图，不是完整 Token 表）：`#333333`、`#999999`、`#1677FF`、`#FFFFFF`、`#FF6430`。字体：PingFang SC Regular / Medium / Semibold；数字 DINPro-Medium / Alibaba Sans。

外来 Symbol（Kitchen / Alipay）：Toast、Mask、StatusBar、返回按钮、人保 logo、Home Indicator。这些是支付宝基础件，不是理赔自建组件。

**还需要你发的 Sketch（下列标签对应的源文件）：** 优先拖 `.sketch` 进对话（当文件，不要截成图）；多个可以打成一个 zip。GitHub 单文件建议 < 50MB。

**门户**

- 门户（向导阵地页）
- 金额=0 / 金额>0
- 旧版理赔门户
- 有理赔记录 / 无理赔记录
- 首次开箱弹窗
- 个性化卡片：理赔进度 / 热门疾病+医院引导 / 热门疾病+关怀 / 先进药械 / 就医快捷报销 / 经验之谈 / 兜底样式
- T+0～T+25 / T+26～T+30 / 多进度

**进度与结论**

- 理赔申请已关闭/已取消
- 理赔审核未通过（智能解读版 / 普通版）
- 理赔审核通过-已打款 / 待打款 / 赔付零结（有解读版 / 通用版）
- 理赔拒赔：混合原因 / 医院不符合 / 一般免责 / 纯门诊 / 既往症 / 等待期 / 重复理赔 / 非保期 / 材料不齐
- 异常情况：保险公司 reject-reason 为空
- 未订阅 / 已订阅 / 快捷报销可使用
- 安心赔卡片 / 理赔通知书支持下载

**申请向导（方式一：理赔说明页）**

- 保单浮层 / 预申请 / 模式选择 / 医院选择 / 上传材料 / 再次询问 / 材料检索 / 补材卡片 / 出险信息确认 / 基础信息确认 / 签名 / 提交完成 / 材料必传字段确认卡

**方式二：小保内发起**

- 历史出险医院 / 线上已有流程 / 有历史就诊单选 / 首次就诊

**评估助手 / 疾病选择**

- 有安心赔 / 无安心赔
- 甲状腺癌 / 肠胃炎 / 疝气 / 未确诊 及对应编辑浮层
- 家人疾病选择 mock 页

---

## 2. 原生 Component / Instance 清单

### 2.1 本地 Component / Component Set

| 文件 | 结果 |
| --- | --- |
| 理赔侧设计规范 | **Published components = 0**。未发现本地 Component Set。 |
| Sketch 导入 | 仅 1 个已发布 Component Set：`Component 6` `201:3414`。变体名 `Property 1=Frame / Frame 17`，另有 TEXT 属性 `就医类型`。**命名无业务语义，不能当作正式理赔组件。** 出现 8 次。 |

Sketch 导入中还有未发布/未命名 Instance：`Component 2`×9、`Component 3`×9、`Component 5`×25。名称无语义，**待人工确认它们实际是什么**。

### 2.2 外部库 Instance（可识别，但多数不是理赔业务组件）

| 组件名 | 出现次数（历史稿 / 最新流程 / Sketch） | 是否可直接复用到理赔 DS | 说明 | Evidence |
| --- | --- | --- | --- | --- |
| 导航/顶部导航 TopBar/浅色 | 25 / 16 / 12 | 仅作导航参考 | 浅色 TopBar，非理赔蓝头 | L1 |
| 全局遮罩 Overlay | 16 / 13 / 7 | 可复用遮罩模式 | Bottom Sheet / Dialog 底层 | L1 |
| @弹框/关闭/深色 | 15 / 13 / 0 | 可复用关闭图标 | 36×36 | L1 |
| 操作/按钮 Button | 6 / 8 / 1 | **否** | 画布流程标注条，非产品按钮 | L1 结构 / L4 用途 |
| 反馈/轻提示 Toast | 1 / 1 / 0 | 可参考 | 仅 1 个实例，不足以定规范 | L1 存在 / L2 不足 |
| 添加疾病 | 2 / 2 / 7 | 候选 | 疾病选择附加模块 | L1 |
| 图标｜plus｜disease-option｜乳腺结节 | 10 / 10 / 0 | 候选 | 疾病选项加号，名称被锁在「乳腺结节」 | L1 |
| Top Barrier / Down Barrier | 少量 / 少量 / 16+13 | 仅小程序/H5 壳 | 评估助手页系统栏 | L1 |
| 图标/状态图标 StatusIcon | 0 / 0 / 1 | 不足 | 仅 1 次 | L1 |
| 人保 白色 及备份 | 历史稿 5 | Page-specific | 保司 logo，不是通用组件 | L1 |
| Check-one (校验) / Plus (加) | 各 1 | 不足 | 图标实例 | L1 |

Variables：对页面节点调用 `get_variable_defs` 无本地选择结果。颜色/字号 **本阶段不提取为 Exact Token**。

---

## 3. 隐性组件清单 Implicit Components

这些是 Frame / Group / 重复结构，不是 Component。判断为 Candidate 或 Core 的，进入后续组件化。只出现一次的标 Page-specific。

| 组件 | 结构证据 | 出现 | 分类 | 使用场景 | 是否可直接提取尺寸 | Evidence | 优先级 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Bottom Sheet Selector | named `BottomSheet` + `SheetHeader` | 历史 10 / 流程 8 | **Core** | 就诊医院、疾病选择 | 容器可测；内部部分图片 | L2 | P0 |
| SearchBar | named `SearchBar` / `search-box-multiselect` | 8+ | **Core** | 医院搜索 | 可测 | L2 | P0 |
| Hot Search Pills | `SectionHotSearch` + `HotSearchPillsGrid` | 3+ | **Core** | 历史搜索 / 热搜医院 | 可测 | L2 | P0 |
| Selected Chip | `ActiveSelectedChip` / `selection-tag` / `disease-chip` | 17+14+5 | **Core** | 已选医院/疾病/就医类型 | 可测 | L2 | P0 |
| Selection Confirm Panel | `SelectionConfirmPanel` + `ConfirmButton` | 8 | **Core** | 选择器底部确认 | 可测 | L2 | P0 |
| Form Row Selector | Label + Value + Chevron，未 Component 化 | 申请步骤截图中大量；疾病查查少量可编辑 | **Core** | 就诊医院、疾病、时间、类型 | 截图内不可 Exact | L3 主 / L2 结构 | P0 |
| Segmented Control | 疾病 / 意外 双选项 | 申请步骤2 截图 | **Core** | 事故类型 | 截图 | L3 | P0 |
| Primary / Secondary Button Pair | 暂存 + 提交信息 + 取消申请 | 申请步骤截图稳定出现 | **Core** | 向导提交 | 截图 | L3 | P0 |
| Pill Primary Button | 「我知道了」「选它」「立即补充」 | 弹窗/方式选择/预审 | **Core** | 阻断确认、主操作 | 截图+少量可编辑 | L2/L3 | P0 |
| Claims Portal Card | 白卡片 + 标题 + 主按钮 | 理赔门户、我的入口 | **Core** | 门户模块 | 部分可测 | L2 | P0 |
| Step / Progress | 3 步申请进度；4 步了解流程 | 申请步骤、理赔说明 | **Core** | 申请向导 | 截图 | L3 | P0 |
| Upload Dropzone | 虚线框 + 相机 + 批量上传 | 申请步骤3 | **Core** | 材料上传 | 截图 | L3 | P0 |
| Material Category Card | 标题 + 必须/有则提供 Tag + 示例 + 缩略图 + 删除/移动 | 申请步骤3 | **Core** | 发票/病历/出院小结 | 截图 | L3 | P0 |
| Upload Thumbnail Overlay | 图片 + 删除 \| 移动 | 申请步骤3 | **Candidate** | 已传材料操作 | 截图 | L3 | P0 |
| Dialog / First-open Modal | 首次开箱弹窗 | 流程 `20:1743`、Sketch 标签 | **Core** | 理赔向导介绍 | 可部分读取 | L2 | P0 |
| Diagnosis Bottom Sheet | 智能材料诊断 | 理赔预审 `22:3413` | **Core** | 缺材/低置信 | 视觉识别 | L3 | P0 |
| Claims Record Card | 时间 + 产品名 + 保司 + 被保险人 + 底栏状态 | 理赔记录截图 | **Core** | 记录列表 | 截图 | L3 | P0 |
| Status Banner | 申请已关闭 / 审核未通过 / 待评价 | Sketch 进度页 | **Core** | 进度结论 | 截图 | L3 | P0 |
| Progress Timeline | 提交申请 → 材料初审 → 理赔审核 | Sketch 申请进度 | **Core** | 进度详情 | 截图 | L3 | P1 |
| Confirmation / Signature | 授权文案 + 点击签名 + 主按钮 | 签名协议截图 | **Core** | 提交确认 | 截图 | L3 | P0 |
| Toast | 请完整阅读后再签署 | 签名页 | **Candidate** | 阅读拦截 | 截图 + 1 个 Instance | L3/L1 | P1 |
| Scroll Hint Pill | 请滑动并完整阅读 | 签名页 | **Candidate** | 长协议 | 截图 | L3 | P1 |
| Info Tooltip | 免赔额说明气泡 | 申请步骤2 | **Candidate** | 字段说明 | 截图 | L3 | P1 |
| Numbered Q&A Block | 1. 什么情况下可赔 | 疾病查查 | **Candidate** | 可赔说明 | 部分可编辑 | L2 | P1 |
| Context Capsule | 母亲*洁 若患甲状腺癌 + 编辑 | 疾病查查 | **Candidate** | 查询上下文 | 可测 | L2 | P1 |
| 安心赔 Badge | 安心赔优秀认证 / 卡片角标 | 门户、说明页 | **Candidate** | 品牌标识 | Mixed | L2/L3 | P1 |
| Calendar | named `calendar` | 8 / 3 / 2 | **Candidate** | 就诊时间 | 有 named frame，完整态多在图里 | L2 名称 / L3 视觉 | P1 |
| Unselected Radio | `元素/选择/未选中` | 12 / 0 / 4 | **Candidate** | 单选医院/保单 | 可测 | L2 | P1 |
| MultiAction Dialog | `浮层/多按钮弹窗 MultiActionDialog` | 8 | **Candidate** | 多操作弹窗 | named frame | L2 | P1 |
| Bottom Tab | `底部tab` | 2 | Page-specific to 我的页 | 支付宝底栏 | 入口页 | L3 | P2 |
| 车险权益对比 Dialog | Sketch `image 1` | 1 | **Page-specific** | 车险，非医疗险主链路 | 截图 | L3 | P2 |
| 分享浮层 | 老带新 | 流程图片 | **Page-specific** | 增长，非理赔主组件 | 截图 | L3 | P2 |

### Selector / Radio / Checkbox / Switch 边界（仅盘点，不定规范）

| 控件 | 项目中的真实用法 | 证据 |
| --- | --- | --- |
| Selector（行选择） | 医院、疾病、时间、证件上传入口 | L2/L3 |
| Bottom Sheet Selector | 医院搜索选择、热搜、多选 chip | L2 |
| Segmented（类 Radio） | 事故类型：疾病 / 意外 | L3 |
| Checkbox | `checkbox-circle-fill` 用于列表选中/完成，不是表单勾选协议 | L2 |
| Switch | **本阶段未发现稳定 Switch 组件。** 待人工确认是否存在 | — |

---

## 4. 图片 / Screenshot / Flattened UI 清单

统计口径：名称含 `image`，宽约 750，高 ≥ 1400 的节点。

| 文件 | 全屏图片数量 | 说明 |
| --- | --- | --- |
| 最新理赔业务流程 | **22** | 申请主链路几乎全是图 |
| 理赔历史稿 | **51** | 与 Sketch 有重复导入痕迹 |
| Sketch 导入 | **121** | 全链路主资产 |
| 小图 image 11 等 | 大量 37×38 | 看起来是图标位图，不是屏幕 |

### 4.1 最新流程中必须当图片处理的屏幕

| 父屏幕 | 图片节点 | 视觉识别出的内容 |
| --- | --- | --- |
| 选择申请方式 `22:2998` | `image 14` `22:2815` | 理赔说明页 + 底部双卡选择 Bottom Sheet |
| 申请步骤1 `22:2999` | `image 15` `22:3002` | 基本信息表单、证件上传行、双按钮 |
| 申请步骤2-疾病 `22:3008` | `image 16` `22:3006` | 分段、Tag 选择器、金额、长文本 |
| 申请步骤2-意外 `22:3012` | `image 17` `22:3010` | 意外态表单 |
| 申请步骤3 | `image 18/19/20` | 上传、材料分类、缩略图 |
| 签名协议 / 签名 | `image 21/22` | 授权、签名槽、Toast |
| 保单详情 / 互动式理赔 | `image 13/12` | 入口 |
| 理赔记录 / 运费险 | `image 23/24/25` | 记录卡、状态条 |
| 分享系列 | `image 26–29` | 增长页 |

### 4.2 Flattened 但不是整屏图

- `我的-理赔入口`、`理赔门户`：大量 Mask/Vector，图层可点，但很多是展开后的布尔/蒙版，**颜色和圆角不要当 Exact Token 用**，需抽样实测后再进 L1。
- 就诊医院 Bottom Sheet：结构是 Frame，部分装饰/键盘/插图是 image。

---

## 5. 图片中识别出的候选组件

全部标记 **视觉识别 / 需要人工复刻**。置信度只表示“这是不是这个组件”，不表示尺寸已确认。

### P0 必须进入 DS 候选

| 识别名 | 所在 | 状态可见 | 置信度 |
| --- | --- | --- | --- |
| Primary Button（胶囊蓝底白字） | 门户申请、弹窗我知道了、选它、立即补充、确认授权 | Default | High |
| Secondary Button（白底描边「暂存」） | 申请步骤 1/2/3 | Default | High |
| Text Button（「取消申请」「诊断有误，忽略」） | 申请步骤、预审 | Default | High |
| Form Row / Selector | 为谁申请、医院、时间、疾病、证件 | Default / Filled / Chevron | High |
| Required Asterisk | 申请人电话等 | Default | High |
| Segmented Control 疾病/意外 | 步骤2 | Selected / Unselected | High |
| Removable Tag | 住院、医院名、疾病名 | Selected + close | High |
| Date Selector | 就诊时间 | Filled | High |
| Amount Input | 就诊费用 + 元 | Filled | High |
| Long Text + Counter | 病情描述 47/500 | Filled | High |
| Nav Bar 蓝底 | 理赔申请 / 理赔说明 / 申请进度 | Default | High |
| Stepper 3 步 | 基本信息 / 就医情况 / 上传材料 | Pending / Current / Done | High |
| Upload Dropzone | 批量上传，智能分类 | Empty | High |
| Material Card | 必须提供 / 有则提供 | Empty / Has files | High |
| Thumbnail + 删除/移动 | 发票、病历 | Uploaded | High |
| Method Choice Sheet | 向导协助 vs 自助申请 | Default | High |
| First-open Dialog | 理赔向导 | Default | High |
| Diagnosis Sheet | 缺 1 项 / 立即补充 | Missing material | High |
| Record Card + Status Bar | 审核未通过 / 待评价 | Fail / Action | High |
| Signature Box | 点击签名 | Empty | High |
| Hospital Result Row | 高亮关键字 + 三级甲等 Badge + 地址 | Default / Long text | High |

### P1 建议复刻

| 识别名 | 所在 | 置信度 |
| --- | --- | --- |
| Boxed Statistic Digits | 累计帮助 1286 万人次 | Medium |
| Portal Guarantee 2×2 Grid | 认证标准 | Medium |
| Progress Timeline | 申请进度详情 | High |
| Closed Status Gradient Banner | 申请已关闭 | High |
| Claims Guide Reminder Card | 关闭原因说明 | High |
| Star Rating | 请评价本次申请 | Medium |
| Scroll-to-read Hint | 橙色胶囊 | Medium |
| Deductible Tooltip | 步骤2 | Medium |
| Promo Banner on Records | 安心赔·理赔向导 | Medium |
| Reject-reason Status variants | Sketch 拒赔系列 | Medium（文案变体多，组件是否合并待确认） |

### P2 页面特殊 / 非医疗险主链路

| 识别名 | 所在 | 建议 |
| --- | --- | --- |
| 支付宝底 Tab | 我的-理赔入口 | 不进理赔 DS |
| 车险权益对比表 Dialog | Sketch image 1 | 不进医疗险主规范，除非确认同产品 |
| 老带新分享 / 口令 | 最新流程 | 增长模块，Page-specific |
| 规划服务 / 保险管家卡片 | 我的入口 | 非理赔组件 |
| 评估助手 TopBarrier 代码导出层 | Sketch agent 页 | 另一条产品线 |

未识别名称的图标：一律用「业务图标 A/B…」进入补录，不猜名字。本阶段已见表层图标（返回、客服、记录、关闭、搜索、相机、编辑、时钟、星星），具体 SVG 未提取。

---

## 6. Manual Reconstruction List

> 规则：历史设计中存在，但当前 Figma 无法直接提取为可维护 Component 的，全部进入本表。
> 参数凡无法从原生节点确认，只写 Visual Estimate，并标 ⚠ 待人工确认。

### P0 — 必须人工复刻

#### MR-01 Button / Primary + Secondary + Text

- 组件名称：Button
- 所在页面：申请步骤1/2/3、门户、首次弹窗、方式选择、预审、签名；**原生结构在本地 Sketch 信息填写页**
- 原始来源：Sketch ZIP `按钮/蓝色/可操作`（L1）；最新流程截图作对照（L3）
- 图片位置：Figma `22:3002` `22:3006` `22:3020` `20:1743`；Sketch 吸底组合
- 推断类型：Button
- Sketch Exact（2x / 1x pt）：成对胶囊 **339×98 / 169.5×49**，圆角 = 高度一半。Primary 填充 `#1677FF`，字「提交申请」PingFang SC Regular 36/`#FFFFFF`。Secondary 填充 `#FFFFFF`、描边 `#E5E5E5` 2px，字「暂存」PingFang SC Regular 36/`#333333`。文字按钮「取消申请」26/`#1677FF`。线框胶囊 Symbol 144×49、圆角 8（2x）。
- 最新流程截图：主按钮有时是全宽胶囊（「提交信息」），与 Sketch 成对 50/50 不完全同一规格。**冲突时先记两条，不把截图估高写进 Token。**
- 状态：Default。Pressed / Disabled / Loading **未在本次抽样中确认**
- 使用场景：理赔申请、我知道了、选它、提交信息、暂存、取消申请
- 纳入 DS：是 / Core
- 置信度：High
- Evidence：L1 Sketch 成对按钮 + L3 申请链路截图 + L2 门户重复

#### MR-02 Selector / 表单选择行

- 组件名称：Selector
- 所在：申请步骤1/2、理赔说明页内嵌表单预览
- 来源：`image 15/16`；结构同类在疾病查查可编辑稿中重复
- 推断类型：Selector（Label + Value + Chevron）
- 解剖：① Label ② Value ③ Arrow ④ Row ⑤ 必填 *
- 尺寸：Visual Estimate 行高约 88–104（750 稿，即约 44–52pt）。⚠ 待人工确认，禁止写成 Height = 48px
- 状态：Default / Filled / Chevron 可点。Focused / Error / Disabled / Readonly / Loading **待人工确认**
- 场景：就诊医院、疾病名称、就医时间、证件上传、为谁申请
- 纳入 DS：是 / Core
- 置信度：High
- Evidence：L3 + L2 结构

#### MR-03 Bottom Sheet Hospital Selector

- 组件名称：BottomSheet Selector / 就诊医院
- 所在：历史稿 `5:1280` `5:1740`；流程同类
- 来源类型：Implicit Frame + 部分 image（键盘、装饰）
- 可识别结构：SheetHeader 标题「就诊医院」+ 关闭；SearchBar；历史搜索/热搜 Pills；结果列表；关键字高亮；医院等级 Badge；超长省略
- 状态：Default / Searching / Result / Long-text
- 场景：医院选择
- 纳入 DS：是 / Core
- 可直接提取：结构是，完整视觉态不完全是
- 置信度：High
- Evidence：L2 结构 / L3 列表视觉

#### MR-04 Input / Amount + Long Text

- 组件名称：Input
- 所在：申请步骤2 `image 16`
- 类型：Amount（300 元）、Long Text（病情描述 + 47/500）
- 状态：Filled。Empty / Error / Disabled ⚠ 待人工确认
- 场景：就诊费用、事故描述
- 纳入 DS：是 / Core
- 置信度：High
- Evidence：L3

#### MR-05 Upload / 材料上传

- 组件名称：Upload
- 所在：申请步骤3 `image 18/19/20` `22:3025`
- 识别状态：Empty dropzone；分类卡空态；已上传缩略图；删除；移动
- **未见独立图层的状态：** 上传中、识别中、失败、缺失、错误、重新上传。这些在预审浮层和 Sketch 补材标签里有业务存在，但 **组件态未提取成功**
- 材料类型：医疗发票、住院病历、出院小结、其他补充材料。身份证在步骤1以 Selector 行出现
- 纳入 DS：是 / Core
- 置信度：High（空/已传） / Medium（过程态）
- Evidence：L3
- ⚠ 过程态待人工从 Sketch「上传材料 / 材料检索 / 补材卡片」图中补确认

#### MR-06 Confirmation / 签名授权

- 组件名称：Confirmation + Signature
- 所在：`22:3048` `image 21`
- 展示：授权文案、被保险人签字槽、日期、修改申请信息、确认授权完成申请
- 可改：修改申请信息。返回：导航返回。提交：主按钮
- Toast：请完整阅读后再签署
- 纳入 DS：是 / Core
- 置信度：High
- Evidence：L3

#### MR-07 Dialog vs Bottom Sheet

- Dialog：首次开箱「理赔向导」、车险权益表（P2）、部分居中「我知道了」
- Bottom Sheet：选择申请方式双卡、就诊医院、智能材料诊断、疾病说明浮层
- 边界（仅观察，不定最终规范）：阻断介绍/高风险确认更偏 Dialog；选择/详情/补材更偏 Sheet
- Evidence：L2/L3
- 优先级：P0

#### MR-08 Feedback / Status

- 提交/审核结论主要在 Sketch 图片：关闭、未通过、已打款、待打款、零结、拒赔多原因
- 最新流程可见：记录卡底栏「理赔审核未通过」「待评价」
- 预审：缺失材料橙字 + 立即补充
- Empty：医院搜索无结果文案在可编辑稿中存在（「你输入的中医药医院暂未被收录」）
- Loading：选择器有「搜索中」帧，上传 Loading ⚠ 未在截图中确认
- 纳入 DS：是 / Core
- 置信度：High（结论类型存在） / Low（每一种的精确视觉 token）
- Evidence：L3

#### MR-09 Step / Progress

- 申请 3 步：填写基本信息 / 填写就医情况 / 一键上传材料
- 说明页 4 步：提交申请 / 材料初审 / 理赔审核 / 赔付打款
- 进度页时间轴：提交 → 初审 → 审核，含补材子节点
- 纳入 DS：是 / Core
- Evidence：L3
- ⚠ 三种 Progress 是否合并为一个组件，待人工确认

### P1 — 建议人工复刻

| ID | 组件 | 来源 | 置信度 | 备注 |
| --- | --- | --- | --- | --- |
| MR-10 | Search Result Row + Grade Badge | 就诊医院搜索完 | High | 超长文案省略已出现 |
| MR-11 | Record List Card | 理赔记录 image 23 | High | 底栏状态色分信息蓝 / 任务橙 |
| MR-12 | Portal Stats Digit Boxes | 理赔门户 | Medium | 可能是营销模块 |
| MR-13 | 安心赔 Badge / 认证条 | 说明页、入口 | Medium | 品牌，不是表单控件 |
| MR-14 | Timeline | Sketch 申请进度 image 7 | High | |
| MR-15 | Reject Reason Pages | Sketch 拒赔系列标签 | Medium | 先确认是 Status 变体还是独立页 |
| MR-16 | Calendar Picker 完整态 | named calendar + 截图 | Medium | 完整滚轮/月历 ⚠ 未在本次高清抽样钉死 |
| MR-17 | MultiActionDialog | named frame ×8 | Medium | 需打开具体帧确认内容 |
| MR-18 | Toast | Instance 1 + 签名截图 | Medium | 样本太少 |
| MR-19 | 个性化门户卡片组 | Sketch 门户标签 | Medium | 进度/疾病/医院/先进药械/快捷报销/经验/兜底 |

### P2 — 页面特殊

| ID | 组件 | 来源 | 建议 |
| --- | --- | --- | --- |
| MR-20 | 支付宝底 Tab / 我的页非理赔卡 | `20:1214` | 不进理赔 DS |
| MR-21 | 车险理赔权益对比 Dialog | Sketch `1:4115` | 待确认产品范围 |
| MR-22 | 分享口令 / 微信分享 | 最新流程 | 增长 |
| MR-23 | 评估助手代码图层页 | Sketch smart-notify 页 | 另一产品 |

---

## 7. Component Inventory（汇总表）

| Component | 来源 | 来源类型 | 出现 | 已有 Figma Component | 可直接复用 | 需人工重建 | 场景 | 状态（已见 / 未见） | 优先级 | Evidence | 备注 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Button | Sketch 信息填写 + 最新申请链路 | Sketch Native + Image | 高 | Sketch 有 `按钮/蓝色/可操作` group，Figma 无业务 Component | Sketch 成对按钮是 | 全宽/小尺寸/状态仍要补 | 提交/暂存/知道了 | Default；Disabled/Loading 未见 | P0 | L1 Sketch / L3 截图 | 不要用标注条当规范 |
| Selector | 申请表单 + 医院选择 | Image + Implicit | 高 | 否 | 结构部分是 | 是 | 医院/疾病/时间 | Default/Filled/Search；Error 未见 | P0 | L2/L3 | 理赔最高频 |
| Input | 步骤2 | Image | 中 | 否 | 否 | 是 | 金额/描述/手机号 | Filled；Error 未见 | P0 | L3 | 手机号在步骤1是只读值还是 Input ⚠ |
| Upload | 步骤3 + Sketch 补材 | Image | 高 | 否 | 否 | 是 | 发票病历等 | Empty/Uploaded；过程态未见 | P0 | L3 | |
| Confirmation | 签名协议 | Image | 中 | 否 | 否 | 是 | 提交授权 | Empty signature | P0 | L3 | |
| Dialog | 首次弹窗 | Implicit + Image | 中 | 否 | 部分 | 是 | 开箱介绍 | Default | P0 | L2 | |
| Bottom Sheet | 医院选择/方式选择/预审 | Implicit + Image | 高 | 否 | 结构是 | 部分 | 选择/诊断 | Default/Search | P0 | L2/L3 | |
| Feedback Toast | 签名页 + 1 Instance | Image + Native | 低 | Toast Instance 有，样本 1 | 弱 | 是 | 阅读拦截 | Default | P1 | L1/L3 | |
| Status | 记录卡 + Sketch 结论 | Image | 高 | 否 | 否 | 是 | 关闭/拒赔/打款 | 多种文案 | P0 | L3 | |
| Step / Progress | 申请头 + 说明页 + 时间轴 | Image | 高 | 否 | 否 | 是 | 向导 | Pending/Current/Done | P0 | L3 | 可能是 3 个模式 |
| Nav Bar | 全链路 | Native TopBar + 蓝底图 | 高 | 浅色 TopBar 有；蓝底没有 | 浅色可参考 | 蓝底需重建 | 理赔申请头 | Default | P0 | L1/L3 | |
| Overlay | Sheet/Dialog 底层 | Native Instance | 高 | 是（外部库） | 可参考 | 否 | 遮罩 | Default | P1 | L1 | |
| Chip / Tag | 医院热搜、已选疾病 | Implicit | 高 | 否 | 结构是 | 是 | 多选回填 | Default/Active/Remove | P0 | L2 | |
| SearchBar | 医院选择 | Implicit | 高 | 否 | 结构是 | 少量 | 医院搜索 | Default/Active/Clear | P0 | L2 | |
| Record Card | 理赔记录 | Image | 中 | 否 | 否 | 是 | 历史案件 | Fail/Action | P1 | L3 | |
| 安心赔 Badge | 门户/说明 | Mixed | 中 | 否 | 否 | 是 | 品牌 | Default | P1 | L2/L3 | |
| Calendar | 就诊时间 | Implicit name + Image | 中 | 否 | 否 | 是 | 日期 | 完整态待确认 | P1 | L2/L3 | |
| Empty | 医院未收录文案 | Implicit 文案 | 低 | 否 | 文案是 | 是 | 搜索无结果 | 1 个文案 | P1 | L2 | 插画空态未在本次确认 |
| Switch | — | — | 0 | 否 | — | 待确认 | — | 未见 | — | — | 不要编造 |
| Checkbox 协议勾选 | — | checkbox-circle-fill 被用于完成态 | — | 否 | 否 | 待确认 | 可能不是协议勾选 | 未见独立协议 Checkbox | P2 | L2 误用风险 | |

---

## 8. 优先级总表

### P0 下一阶段必须处理

1. Button（主/次/文字）
2. Selector（行选择 + Bottom Sheet 医院/疾病）
3. Input（金额、长文本；手机号待确认）
4. Upload（分类卡 + 缩略图；过程态补录）
5. Confirmation / Signature
6. Dialog（首次开箱）与 Bottom Sheet 边界
7. Status / 预审缺材 Feedback
8. Stepper
9. 蓝底 Nav Bar（与现成浅色 TopBar 分开记录）

### P1

Record Card、Timeline、Toast、Calendar 完整态、安心赔 Badge、门户营销数字、拒赔原因是页还是 Status 变体。

### P2

我的页底 Tab、车险 Dialog、分享裂变、评估助手代码页、保司 Logo。

---

## 9. 本阶段明确不写进正式 Token 的东西

- 任何从截图估的 px / HEX / 字号 / 圆角（Sketch JSON 读出的除外，且须标明 2x）
- Ant Design / Material 默认值
- Switch、协议 Checkbox、Upload Loading 等未见控件
- `操作/按钮 Button` 标注条的尺寸
- `Component 2/3/5/6` 无语义组件的业务定义

## 10. 和最新业务流程的关系

最新流程证明主任务仍是：

入口（我的 / 保单 / 门户）→ 说明/方式选择 → 三步申请 → 签名 → 预审补材 → 记录/进度结论。

历史 Sketch 补充了最新稿截图里缺失的 **过程态和结论态**（拒赔原因矩阵、关闭、打款、补材卡片、材料检索）。

两者冲突时：以最新业务流程的页面层级为准，用历史稿补状态，不把旧版门户个性化卡片直接升成 P0。

---

## 11. Prompt 优化（已用于本次盘点，供你确认）

1. Sketch 导入按独立源扫描，Symbol 丢失则整屏进 Manual Reconstruction。
2. named Frame 包整张图 = Image，不因为 Frame 有名字就当 Native Component。
3. 画布标注组件与产品组件分开。
4. 车险 / 我的页 / 增长分享默认 P2，除非你确认同属这套 DS。
5. 不见过程态就写「未见」，不补 Loading/Error 假数据。

---

## 12. 请你确认后再进入 Phase 02

请确认这几件事：

1. 范围是否只做 **医疗险理赔**，车险、评估助手、老带新是否排除。
2. `Component 2/3/5/6` 是否有你知道的真实含义。
3. 申请步骤 1–3 是否就是当前线上主视觉；若是，P0 复刻以这些截图为准，Sketch 成对按钮作 Exact 尺寸源。
4. 是否接受「最新流程主链路 = 图片源；本地 Sketch = 原生图层源」这一判断。
5. 其余本地 Sketch 请继续拖进对话（当文件，不要截成图）。Figma 授权不能代替读你磁盘。

确认后才开始 Phase 02 Foundation。本阶段到此停止。
