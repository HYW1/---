# Plugin API 陷阱

配合 `figma-use`。数字例子来自一次步骤条还原，规则本身不绑业务。

## 页面与脚本

- 每次调用从文件第一页开始。用 `await figma.setCurrentPageAsync(page)`，禁止赋值 `figma.currentPage`。
- **一次脚本只切一次页。** 多页拆成多次并行 `use_figma`。
- 必须 `return` 变更过的 node id。`figma.notify`、`console.log` 不可用。
- 写操作必须串行，禁止并行 `use_figma` 改同一文件。
- 禁止编造 node id；只用上一次 return 或 `getNodeById` 读到的。
- 颜色 `{r,g,b}` 是 **0–1**。`#1677FF` → `{ r: 22/255, g: 119/255, b: 1 }`。

## 字

- 改任何 TEXT 前：`getStyledTextSegments(['fontName'])` → `loadFontAsync` → 再改。
- 字体跟**该产品规范**：中文常见 PingFang SC；数字可能是 Inter / 品牌数字体。不要混用。
- 行高默认 AUTO。自定义 PIXEL 行高容易把标题/芯片撑乱。

## Auto Layout vs Absolute

- 有结构关系的用 `figma.createAutoLayout()`。
- 连线、光晕、气泡：`layoutPositioning = 'ABSOLUTE'`。先挂到父级再设 Absolute，再设 x/y。
- `layoutSizing*` 是 `FIXED | HUG | FILL`；轴模式是 `FIXED | AUTO`。不要混。
- FILL 只能给已经在 AL 父级里、且不是 Absolute 的子节点。
- 装饰线 **z 在内容下**：`insertChild(0, line)`。否则线会画在小圆旁边的透明热区里。

## resize

小图形居中在大热区时：

```js
// 错：外框和装饰一起被放大
comp.resize(85, 85);

// 对：外框不约束缩放；内圆保持原稿尺寸并居中
comp.resizeWithoutConstraints(85, 85);
oval.resize(60, 60);
oval.x = 12.5;
oval.y = 12.5;
```

## 变体与属性

- 图层名声明轴：`状态=当前` 或 `状态=步骤2, 2到3=半段白`。
- TEXT 属性加在 **COMPONENT_SET** 上，不要对单个变体的 `componentPropertyDefinitions` getter 动手（会丢）。
- `componentPropertyReferences` 只能设在主组件图层，不能设在 INSTANCE 内部。
- 同一 TEXT 属性全局一个 `defaultValue`。目录上的 1/2/3 用 `instance.setProperties`。
- `isExposedInstance`：实例进父组件之后再 `true`。
- 克隆变体进同一 SET 再改名，可加第二轴。目录放不下就 `visible = false`，实例仍可切。

## 量原稿

每个溯源节点 dump：`x, y, width, height, fills, strokes, strokeWeight, strokeCap, fontName, fontSize, layoutPositioning, 子树`。  
矢量连线看 **每条** 的 x/w，不要只看编组包围盒（包围盒会把穿模残段算进去）。

## 导入叠线

Sketch / 历史稿常有多条同名线叠在一起。先截图看产品看见几段、什么颜色，再画 2～3 条等价 VECTOR（注意 cap / weight），停在**可见图形边缘**，不要整组 clone。
