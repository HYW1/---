---
name: claims-visual-guard
description: Guardrails for measuring 理赔工具 visuals. Use when extracting tokens or specs from Figma/Sketch/screenshots. Reject garbled text, placeholder frames, wrong layer names, and screenshot guesses.
---

# 理赔工具视觉验收护栏

量规范时先过这套规则。宁可标 L3 / 待确认，也不要把错误稿写成 Exact。

## 必须用

- 原生图层：Figma Plugin API / `get_metadata` / Sketch ZIP JSON
- `figma-design-extract`：从结构化数据出 spec table
- `visual-qa`：只拿截图当对照，不拿像素去估 px/HEX

## 禁止当正确稿

1. **乱码 / 截断 / 叠字**：如 `**成`、单元格里同一病名横向重复、缺字豆腐。
2. **空壳占位**：标题在、内容区整块灰底无文案（如「自定义底部面板」流程说明 Sheet）。
3. **图层名与画面不符**：药品查查文件里大量 `医院查查2备份 *`。以画面文案为准，不以图层名为准。
4. **整屏位图**：名为 `位图` 的 Rectangle。只做 L3 视觉识别。
5. **标注条 Button**：宽几千 px 的流程标注，不是产品按钮。

## 证据等级

| 来源 | 等级 |
| --- | --- |
| Sketch JSON / Figma 可读 TEXT·RECTANGLE·COMPONENT | L1 Exact（2x 画布先 ÷2） |
| 多页重复的稳定结构 | L2 |
| 截图 / 位图 / 视觉模型估尺寸 | L3，禁止写进正式 Token |
| 乱码、占位、错误图层 | **丢弃**，不记为规范 |

## 冲突

同一组件多份稿不一致时：最新业务流程主视觉优先；历史工具稿补状态；尺寸以原生图层为准，不以截图估值为准。
