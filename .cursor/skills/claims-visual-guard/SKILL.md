---
name: claims-visual-guard
description: Guardrails for measuring 理赔工具 visuals. Use when extracting tokens or specs from Figma/Sketch/screenshots. Reject garbled text, placeholder frames, wrong layer names, and screenshot guesses.
---

# 理赔工具视觉验收护栏

量规范时先过这套规则。宁可标 L3 / 待确认，也不要把错误稿写成 Exact。

## 必须用

- 落地组件 / Token：先走 `alipay-app-design-system`（支付宝 APP 基础精简 key）。Figma 按 **750** 画，不要 ÷2。
- 历史稿 `skill`（`ZXibIc4lflyHRoTF7OQV0L`）：只当**体验模式**样本，用基础库组件重建，不抄位图像素。
- 原生图层：Figma Plugin API / `get_metadata` / Sketch ZIP JSON
- `figma-design-extract`：从结构化数据出 spec table
- `visual-qa`：只拿截图当对照，不作 Exact 来源
- 做成可切组件时走 `figma-spec-component-build`（不绑理赔；变体轴、TEXT 属性、原稿还原）

## 禁止当正确稿

1. **乱码 / 截断 / 叠字**：如 `**成`、单元格里同一病名横向重复、缺字豆腐。
2. **空壳占位**：标题在、内容区整块灰底无文案（如「自定义底部面板」流程说明 Sheet）。
3. **图层名与画面不符**：药品查查文件里大量 `医院查查2备份 *`。以画面文案为准，不以图层名为准。
4. **整屏位图**：名为 `位图` 的 Rectangle。只做 L3 视觉识别。
5. **标注条 Button**：宽几千 px 的流程标注，不是产品按钮。

6. **别的蚂蚁设计库**：WorldFirst 🌍、Antom、AlipayHK、飓创。同账号能搜到，**不是**支付宝 APP 基础库。Copy 真源是 `4Q2KGg9fstrN2BWCwYChzi`（未发布，key 无法跨文件导入）。已发布的 APP 基础组件在团队库「信用卡基础组件」（`操作/按钮` + APP token）；不要把信用卡**业务页面**当理赔 Kitchen。
7. **Kitchen 官网下载页**：没有组件尺寸表。
8. **手绘主按钮 / TopBar**：有库 key 时必须 `importComponentSetByKeyAsync`，禁止 Rectangle 冒充 Button。

## 证据等级

| 来源 | 等级 |
| --- | --- |
| 支付宝 APP 基础库可读 Component / Variable | L1，Figma 保持 750 原值 |
| Sketch JSON / Figma 可读 TEXT·RECTANGLE | L1 Exact；Sketch 2x 先 ÷2 才是 pt；**Figma 750 稿不要 ÷2** |
| 多页重复的稳定结构 | L2 |
| 截图 / 位图 / 视觉模型估尺寸 | L3，禁止写进正式 Token |
| 乱码、占位、错误图层 | **丢弃**，不记为规范 |

## 冲突

同一组件多份稿不一致时：最新业务流程主视觉优先；历史工具稿补状态；尺寸以原生图层为准，不以截图估值为准。
