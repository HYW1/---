# Installed design-system skills

## From [`keg-flair/cursor-designer-agents`](https://github.com/keg-flair/cursor-designer-agents)

Vendored at commit `8ba64c4bf3796daa48fccd2895ab4727a5e1e9bc`. MIT: `LICENSE.cursor-designer-agents.txt`.

- `design-specs-writer`
- `component-spec-writer`
- `design-system-governance`

## From [`jeltehomminga/figma-design-skills`](https://github.com/jeltehomminga/figma-design-skills)

MIT: `LICENSE.figma-design-skills.txt`.

- `figma-design-extract`: 从 Figma 结构化数据出 Exact spec，**禁止用截图量 px**
- `design-fidelity-verify`: 后续实现时对照 spec 做视觉验收

## From [`dylanfeltus/skills`](https://github.com/dylanfeltus/skills) `visual-qa/`

- `visual-qa`: 截图对照检查清单。本项目里截图只作对照，不作 Exact 来源。

## Project

- `alipay-app-design-system`：**本仓库默认 Figma / UX 规范。** Token、组件 key、750 画布、历史稿体验模式。禁止手绘 TopBar / 主按钮。换产品时换对应设计系统。
- `figma-spec-component-build`：**做规范 + 做可切组件（不绑业务）。** 变体轴、TEXT 属性、变量绑定、原稿还原 vs 导入垃圾。理赔 / 理财 / 到店 / 另一文件都走同一拆法。
- `c-end-visual-craft`：C 端视觉质感。不重造组件；只做氛围 / 主视觉 / 去 AI 感。
- `claims-visual-guard`: 理赔工具稿护栏。乱码、空壳、图层名错误一律丢弃。仅量那批稿时用。

出 Figma 规范组件时顺序：该产品的设计系统 skill → `figma-spec-component-build` → `figma-use` / `figma-generate-library` → 需要质感时再开 `c-end-visual-craft`。本仓库的设计系统 skill 是 `alipay-app-design-system`。
