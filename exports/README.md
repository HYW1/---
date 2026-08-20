# 导入 Figma Skill

官方说明：Figma agent / Figma Make 的自定义 skill **只接受单个 Markdown 文件**，不支持 `references/`、`scripts/`、`assets/`。

上传文件用这一份：

**[`design-spec-components.md`](./design-spec-components.md)**

## 导入到 Figma（agent / Make）

1. 打开任意 Figma 文件，点聊天框
2. 选 **Skills** → **Add skill**（或 **Upload**）
3. 上传 `design-spec-components.md`
4. 名称保持 `design-spec-components`（斜杠命令：`/design-spec-components`）
5. 确认 description 已带上；不要删 frontmatter

之后在任意文件里说「做规范」「做组件」「还原原稿」，或输入 `/design-spec-components`。

## Cursor / Claude Code

仓库里完整版（含对照例和 API 陷阱分文件）：

`.cursor/skills/figma-spec-component-build/`

不必再导一次；Cursor 会读这个目录。若要拷到 Claude Code：把该文件夹放到 `.claude/skills/design-spec-components/`，主文件仍须叫 `SKILL.md`。

## 和本仓库其它 skill 的关系

- 色板 / 750 / 禁手绘按钮：`alipay-app-design-system`（仅本仓库默认产品）
- 画组件的 API：Figma 的 `figma-use` + `figma-generate-library`
- 本文件：怎么拆规范、怎么做变体，不绑业务
