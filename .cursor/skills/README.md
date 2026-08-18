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

- `alipay-app-design-system`：**默认 Figma / UX 规范。** Token、组件 key、750 画布、历史稿体验模式。禁止手绘 TopBar / 主按钮。
- `c-end-visual-craft`：C 端视觉质感。不重造组件；只做氛围 / 主视觉 / 去 AI 感。
- `claims-visual-guard`: 理赔工具稿护栏。乱码、空壳、图层名错误一律丢弃。

出 Figma 稿时顺序：`alipay-app-design-system` → `figma-use` / `figma-generate-library` → 需要质感时再开 `c-end-visual-craft`。
