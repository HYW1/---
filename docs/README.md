# 理赔业务 Design System — 文档目录

默认规范：`.cursor/skills/alipay-app-design-system`。Figma 按 **750** 画，组件用已发布 APP 基础库实例，不要手绘主按钮。

## 怎么读

- **L1 库实例**：已发布 `操作/按钮` 等 APP 组件 + APP token。Figma 保持 750。
- **L1 Sketch**：本地 ZIP JSON。Sketch 是 **2x**，pt = 数值 ÷ 2；不要把 pt 当 Figma 尺寸。
- **L2 Repeated Pattern**：多页重复，结构可进规范，尺寸仍要复核。
- **L3 Visual Recognition**：整屏截图。只记形态，不写猜的 px。

`#1677FF`（申请按钮）和 `#40B0F8`（查查 Tag）先当两套蓝。

## 已产出

| 切片 | 文件 | 证据 | 状态 |
| --- | --- | --- | --- |
| 盘点 | [phase-01-asset-inventory.md](./phase-01-asset-inventory.md) | 全源扫描 | 冻结作附录 |
| 01 Button | [specs/01-button.md](./specs/01-button.md) | APP Button / ButtonGroup / PageFooter 实例 | [Figma 规范页](https://www.figma.com/design/NiXwro23h7CvvWT7GOb1ep/?node-id=62-14) |

## 接下来

02 Selector → 03 Input → 04 Upload → 05 吸底栏 / Dialog / Bottom Sheet → 06 查查工具页（与申请内选择器分开）

Kitchen 壳（StatusBar、返回、Mask、Toast）只复用，不重做。
