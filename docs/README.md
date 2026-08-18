# 理赔业务 Design System — 文档目录

先写能落地的切片，不一次铺开 Foundation，也不在 Figma 里建库。

## 怎么读

- **L1 Exact**：Sketch JSON 或 Figma 可读图层。Sketch 是 **2x 画布**，pt = 数值 ÷ 2。
- **L2 Repeated Pattern**：多页重复，结构可进规范，尺寸仍要复核。
- **L3 Visual Recognition**：整屏截图上认出来的。只记形态，不写猜的 px / HEX。
- **未见**：不编 Loading / Disabled / Error。

冲突先并列，不合并。`#1677FF`（申请按钮）和 `#40B0F8`（查查 Tag）先当两套蓝。

## 已产出

| 切片 | 文件 | 证据 | 状态 |
| --- | --- | --- | --- |
| 盘点 | [phase-01-asset-inventory.md](./phase-01-asset-inventory.md) | 全源扫描 | 冻结作附录，规范以切片为准 |
| 01 Button | [specs/01-button.md](./specs/01-button.md) | Sketch L1 + 申请链路 L3 | **当前可审** |

## 接下来（未写）

02 Selector → 03 Input → 04 Upload → 05 吸底栏 / Dialog / Bottom Sheet → 06 查查工具页（与申请内选择器分开）→ 07 Foundation Token（你点头后再抽）

Kitchen 壳（StatusBar、返回、Mask、Toast）只复用，不写进理赔组件库。
