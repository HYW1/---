# Plugin API 陷阱（本仓库打过的）

配合 `figma-use`。这里只记规范页组件反复踩的。

## 页面与脚本

- 每次调用从文件第一页开始。用 `await figma.setCurrentPageAsync(page)`，禁止赋值 `figma.currentPage`。
- **一次脚本只切一次页。** 多页就拆成多次并行 `use_figma`。
- 必须 `return` 变更过的 node id。`figma.notify`、`console.log` 不可用。
- 脚本报错 = **整段没执行**。读报错，改脚本，再跑。不要立刻原样重试。
- 颜色 `{r,g,b}` 是 **0–1**，不是 0–255。`#1677FF` → `{ r: 22/255, g: 119/255, b: 1 }`。

## 字

- 改任何 TEXT 前：`getStyledTextSegments(['fontName'])` → `loadFontAsync` → 再改。
- 中文 PingFang SC（Regular / Medium / Semibold）。数字步骤点常用 Inter Regular 30。
- 行高默认 AUTO。自定义 PIXEL 行高容易把步骤标题/芯片撑乱。

## Auto Layout vs Absolute

- 有结构关系的（横排三步、点在上标题在下）用 `figma.createAutoLayout()`。
- 连线、光晕、气泡：`layoutPositioning = 'ABSOLUTE'`。先 `appendChild`/`insertChild` 再设 Absolute，再设 x/y。
- `layoutSizingHorizontal/Vertical`：`FIXED | HUG | FILL`。轴模式是 `FIXED | AUTO`。不要混。
- FILL 只能给「已经在 AL 父级里、且不是 Absolute」的子节点。
- 装饰线要 **压在点下面**：`insertChild(0, line)`，项放后面。否则线会画在 60 圆旁边的透明边里。

## resize

```js
// 错：外框 85，子级 60 圆被一起放大，出现 85 光晕
todo.resize(85, 85);

// 对：外框不约束缩放；圆保持 60，居中
comp.resizeWithoutConstraints(85, 85);
oval.resize(60, 60);
oval.x = 12.5;
oval.y = 12.5;
```

## 变体与属性

- 用图层名声明轴：`状态=当前` 或 `状态=步骤2, 2到3=半段白`。
- **不要**对某个变体主组件的 `componentPropertyDefinitions` getter 去加 TEXT 属性（会丢）。加在 **COMPONENT_SET** 上。
- `componentPropertyReferences` 只能设在 **主组件里的图层**，不能设在 INSTANCE 内部。
- 同一 TEXT 属性全局一个 `defaultValue`。目录上的 1/2/3 必须 `instance.setProperties({ '序号#id': '2' })`。
- `isExposedInstance`：实例进父组件之后再 `true`。
- 克隆变体进同一 COMPONENT_SET 再改名，可加第二轴。目录放不下就 `visible = false`，实例仍可切。

## 量原稿

对每个溯源节点 dump：`x, y, width, height, fills, strokes, strokeWeight, strokeCap, fontName, fontSize, layoutPositioning, 子树`。  
矢量连线看 **每条** 的 x/w，不要只看编组包围盒。包围盒会把穿出圆外的残段算进去。

## 重画连线而不是整组 clone

Sketch 导入常有多条同名 `Line-2备份-*` 叠在一起。产品看见的是：

- 1→2 白：`x=131.5` 宽 `198.5`
- 2→3 白半截：`x=375.5` 宽 `129.5`
- 底 `#6CA0FF` 停在**可见圆的左缘**，不要拷 `w=258.9` 穿到圆心的那条

用 2～3 条 VECTOR（`strokeCap: SQUARE`，weight 4）表达，z 在点下。
