# claude.md — 原型页面制作行为约束（Claude Code 必须严格遵守）

> 本文件规定 Claude Code **如何工作、交付什么、遵守什么红线**。
> 视觉规范（颜色/字号/组件外观）见 `design.md`，本文件**不重复视觉 token**，只要求"引用 design.md，不自造"。
> 页面内容与交互见各模块 `PRD.md`。
> 三者关系：**claude.md 管"怎么做" · design.md 管"长什么样" · PRD 管"这个页面做什么"**。制作任一页面时三份同时读。

---

## 一、角色与目标

你是一名**资深前端工程师**，为"游寄 / 湖滨行李安心游"项目制作**高保真 HTML 原型页面**，交付给开发人员用作视觉+交互还原参考，部分代码可被直接复用。代码必须**规范、语义化、可维护**，不是一次性 demo。

**每个页面的交付标准**：一个自包含、可独立预览、响应式、带真实感 mock 数据、带基础交互、带交互标注的 `.html` 文件。

---

## 二、技术栈（固定，不得擅自更换）

| 项 | 规定 |
|----|------|
| 结构 | 语义化 HTML5 |
| 样式 | **Tailwind CSS via CDN** + 少量内联 `<style>`（token 注入、动画、复杂选择器） |
| 图标 | **Lucide via CDN**（首选），必要时 Font Awesome CDN。**禁用 emoji 代替图标** |
| 脚本 | **原生 JavaScript（ES6+）**。**不使用 Vue / React / jQuery 等框架** |
| 字体 | 按 `design.md` 引入（系统字体 + JetBrains Mono） |

> **关于框架**：本项目原型要求"单文件自包含、双击即预览、无构建步骤"，因此**不使用 Vue/React**（它们需要构建，与单文件预览冲突）。原型交互用原生 JS 实现。若后续改为工程化交付再另行约定。

**CDN 引入（`<head>`）**：

```html
<script src="https://cdn.tailwindcss.com"></script>
<script src="https://unpkg.com/lucide@latest"></script>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600&display=swap" rel="stylesheet">
<!-- 页面底部：lucide.createIcons(); -->
```

- 通过内联 `tailwind.config` 注入 `design.md` 第七章的色板 token；
- 禁止引入任何未列出的第三方库。

---

## 三、视觉规范（引用 design.md，不在此重复）

- **所有**颜色、字号、圆角、间距、组件外观**必须**引用 `design.md`；
- 页面 `tailwind.config` 直接使用 `design.md` 第七章的配置镜像；
- **禁止自造色值/字号/圆角**，禁止偏离 design.md；
- 若 design.md 未覆盖某场景，就近取 design.md 的梯度值，并在代码注释标明。

---

## 四、单文件自包含（强制）

**每个页面 = 一个独立 `.html`**，双击浏览器即可预览，无需构建/本地服务器/外部本地资源（CDN 除外）。

- CSS：Tailwind CDN + 页面内 `<style>`；
- JS：页面内 `<script>`；
- 数据：mock data 内联（见第六章）；
- 图片：用占位（色块/图标/`https://placehold.co`），不依赖本地图片。

**禁止**：外部本地 `.css`/`.js`/图片依赖、构建工具、模块 import。

---

## 五、交互要求（强制，原型必须可交互）

原型不是静态图，以下交互必须真实可用（原生 JS 实现）：

| 交互 | 要求 |
|------|------|
| Tab 切换 | 点击切换内容，选中态高亮 |
| 弹窗 / 抽屉 | 打开/关闭、遮罩点击关闭 |
| 表单校验 | 必填、格式校验，错误提示 |
| hover 态 | 按钮、行、可点元素有反馈 |
| 筛选 / 搜索 | 前端 mock 过滤生效 |
| 下拉 / 日期 | 可展开选择 |
| 页面跳转 | 按钮/菜单跳转对应 `.html`（见第八章） |

组件行为遵循 `design.md` 的组件外观标准。

---

## 六、Mock 数据（强制，让页面真实可信）

- 每个页面用**内联 mock data**（JS 数组/对象）驱动渲染，禁止在 HTML 里堆静态行；
- 数据真实可信、贴合游寄业务：订单号、时间、金额（mono）、手机号（脱敏 `138****8888`）、机柜名、状态等；
- 覆盖多种状态（进行中/待支付/已完成/异常/退款…）以展示不同 Badge；
- 列表至少 8–15 条，体现分页/筛选效果；
- 用 JS 遍历 mock data 渲染，模拟数据驱动。

---

## 七、交互标注系统（强制，本项目特色）

**每个页面必须内嵌"交互标注"，供开发查看每个功能点的交互说明。**

### 7.1 机制

- 在有交互的元素旁放**编号徽标**（小圆标 ①②③…，primary 色，元素右上悬浮）；
- 点击徽标 → **弹出该功能点的完整交互说明**（触发/响应/状态/规则）；
- 页面右边缘设**可拖拽浮动开关**"标注"，一键显/隐所有徽标（预览态 ⇄ 标注态）。

### 7.2 实现

```html
<span class="anno-badge" data-anno="1">1</span>
<script>
const annotations = {
  1: { title: "订单状态筛选", desc: [
    "触发：点击状态下拉选择某状态",
    "响应：表格按所选状态前端过滤刷新",
    "规则：状态为本地映射状态，含’超时寄存中’",
    "默认：进入页面默认’全部’"
  ]},
  // 每个标注一条
};
</script>
```

**标注弹窗**（无蒙版，仅阴影，可拖拽，点击外部关闭）：
```html
<!-- 弹窗：无全页蒙版，仅 box-shadow 区分层级；长按标题栏/拖拽图标可移动；点击弹窗外部关闭 -->
<div id="annoModal" class="hidden fixed z-[300]" style="top:50%;left:50%;transform:translate(-50%,-50%);">
  <div class="bg-white rounded-lg p-6 w-[480px] max-w-[90vw] max-h-[70vh] overflow-y-auto relative"
       style="box-shadow:0 12px 40px rgba(0,0,0,.18);" onclick="event.stopPropagation()">
    <!-- 关闭按钮：绝对定位右上角，20px -->
    <button onclick="closeAnnoModal()" style="position:absolute;top:12px;right:12px;z-index:10;">
      <i data-lucide="x" class="w-[20px] h-[20px]"></i>
    </button>
    <!-- 拖拽手柄：grip-horizontal 图标 + 标题 -->
    <div id="annoDragHandle" style="cursor:grab;" onmousedown="startDragModal(event)" title="长按拖拽移动弹窗">
      <i data-lucide="grip-horizontal" style="opacity:.4;"></i>
      <h3 id="annoModalTitle" class="text-[16px] font-semibold text-ink-title"></h3>
    </div>
    <!-- 说明正文 14px -->
    <ul id="annoModalBody" class="text-[14px] text-ink-body leading-relaxed space-y-2"></ul>
  </div>
</div>
<script>
// 点击弹窗外部关闭
document.addEventListener('click', function(e) {
  var m = document.getElementById('annoModal');
  if (!m || m.classList.contains('hidden')) return;
  if (!m.contains(e.target)) closeAnnoModal();
});
</script>
```

**浮动开关**（右边缘可纵向拖拽，图标区分开关状态）：
```html
<div id="annoToggleWrap" class="fixed z-[150]" style="right:8px;top:120px;cursor:grab;"
     onmousedown="startDragToggle(event)">
  <div class="flex items-center gap-1 px-2.5 py-1.5 rounded-full text-[11px]
       bg-white/90 backdrop-blur text-primary border border-primary/30 shadow-sm">
    <i data-lucide="eye" id="annoToggleIcon" class="w-[13px] h-[13px]"></i> 标注
  </div>
</div>
```

- 徽标：小圆 `20×20px`、primary 底白字、**绝对定位**（`top:-8px;right:-8px`）、z-index 悬浮、hover 放大；**徽标不占文档流，不影响页面布局**；
- 点击徽标 → 弹窗居中显示，**无全页遮罩**（仅弹窗自身带 `box-shadow: 0 12px 40px rgba(0,0,0,.18)` 区分层级）；
- **关闭方式**：① 点击右上角 `×` 关闭按钮（20px）；② 点击弹窗外部页面任意位置自动关闭；
- **弹窗可拖拽**：标题栏左侧有 `grip-horizontal` 拖拽图标（半透明），鼠标长按标题栏或图标 200ms 后拖动；
- **说明文字**：正文 14px，标题 16px，`leading-relaxed` 行距；
- **浮动开关**：位于页面右边缘，默认距顶部 120px；鼠标按住可沿右侧上下拖拽移动；
- **开关图标状态**：标注可见时 `eye` 图标，标注隐藏时 `eye-off` 图标；
- 开关使用 `bg-white/90 backdrop-blur` 半透明设计，减少视觉干扰；
- **说明内容来自该页面对应的模块 PRD**（把 PRD 的交互逻辑/业务规则/状态转写进 `annotations`）；
- 编号页面内唯一、按阅读顺序。

### 7.3 覆盖要求

每个**有交互或有业务规则**的功能点都要标注：筛选、按钮、状态、弹窗触发、表单、跳转、特殊业务规则（两段式防超卖、多退少补、超时补费等）。纯静态展示可不标。

---

## 八、多页面组织与导航（强制）

### 8.1 文件组织

```
/prototype
  ├─ index.html            ← 入口/导航页（汇总所有原型，必做）
  ├─ login.html            ← 登录页（独立页面，无侧边栏）
  ├─ member-management.html ← 成员管理
  ├─ department-management.html ← 部门管理
  ├─ role-management.html  ← 角色管理
  ├─ account-info.html     ← 账号信息
  ├─ message-settings.html ← 消息设置
  ├─ message-center.html   ← 消息中心
  ├─ task-center.html      ← 任务列表
  └─ ...
```

**页面布局（强制）**：除 `index.html` 和 `login.html` 外，所有后台页面**必须**使用标准三段式布局：
- **顶栏**（56px）：左侧 Logo + 系统名，右侧任务列表/消息中心/账号信息图标
- **侧边栏**（220px）：可展开菜单（工作台/订单管理/柜机监控/系统设置/任务列表/消息中心），当前页高亮
- **主内容区**（flex-1，`bg-page` 背景）：内容居中 `max-w-[1280px]`，卡片 `bg-white rounded-lg border`

- 文件名用**语义化英文短横线命名**；
- 页面间用 `<a href>` 或 JS 跳转互通；
- 后台各页共用侧边导航，当前页高亮。

### 8.2 index.html 导航页（必做）

- 汇总所有原型页面，分组（后台系统 / 用户端）；
- 每页一张卡片：页面名 + 简述 + 图标 + "打开"链接；
- 作为交付预览总入口。

---

## 九、响应式（强制）

- 后台面向桌面（≥1280px），必须优雅适配到平板（768px）：侧边栏可折叠、表格 `overflow-x-auto` 横向滚动、不溢出不挤压；
- 用 Tailwind 断点（sm/md/lg/xl）；布局用 Flex/Grid，避免固定像素宽度溢出。

---

## 十、代码质量（交付给开发，须规范）

- **语义化标签**：`<header><nav><main><table><form>` 等，不滥用 `<div>`；
- **结构注释**：区块用注释分隔（`<!-- 筛选区 -->`、`<!-- 订单表格 -->`）；
- **类名规范**：语义化、一致（功能命名/BEM 风格）；
- **JS 组织**：mock data / 渲染 / 交互 / 标注分区，函数拆分，命名清晰，关键逻辑注释；
- **无报错**：控制台无 error，`lucide.createIcons()` 正确初始化；
- **可读可复用**：开发能看懂结构、复用组件片段。

---

## 十一、固定工作流程（每页必守）

1. **读三份**：`claude.md`（本文件）+ `design.md` + 该页面的模块 `PRD.md`；
2. **搭结构**：语义化 HTML + 布局（后台三段 / 用户端手机框）；
3. **套 token**：注入 design.md 的 Tailwind config；
4. **填 mock data**：内联真实感数据，JS 渲染；
5. **做交互**：tab/弹窗/表单校验/hover/筛选/跳转；
6. **加标注**：把 PRD 交互说明转写进 annotations，加徽标 + 说明弹窗 + 全局开关；
7. **接导航**：与 index.html 及相关页互链，侧边栏当前页高亮；
8. **自检**：对照第十二章清单逐条核对；
9. **输出单文件**：双击可预览、无外部依赖、无报错。

---

## 十二、交付前自检清单（每页必过）

- [ ] 单文件自包含，双击可预览，无本地资源依赖（CDN 除外）
- [ ] Tailwind CDN + Lucide，未引入禁用库（无 Vue/React/jQuery）
- [ ] 色值/字号/圆角/间距全部引用 design.md，无自造值
- [ ] 语义色用途正确（primary/success/warning/danger/info）
- [ ] 响应式：桌面正常，平板不溢出，表格可横向滚动
- [ ] Mock data 真实可信、覆盖多状态、≥8 条、数字用 mono
- [ ] 基础交互可用：tab/弹窗/表单校验/hover/筛选/跳转
- [ ] **交互标注完整**：每个交互/规则点有徽标，点击弹说明，全局可显隐
- [ ] 标注内容转写自对应模块 PRD
- [ ] 与 index.html 及相关页互链，侧边栏当前页高亮
- [ ] 语义化标签 + 分区注释 + 规范类名 + JS 分区注释
- [ ] 控制台无 error，Lucide 图标正常渲染
- [ ] 代码规范、可读、开发可复用

---

## 十三、红线（禁止事项）

- ❌ 自造色值/字号/圆角，偏离 design.md
- ❌ 引入 Vue/React/jQuery 或未列出的库
- ❌ 依赖外部本地 CSS/JS/图片（破坏单文件预览）
- ❌ 用 emoji 代替图标
- ❌ 静态堆数据（不用 mock data 驱动）
- ❌ 交互不可用（纯静态图）
- ❌ 遗漏交互标注系统
- ❌ 代码零注释、结构混乱、不可复用

---

## 十四、调用方式

每次制作页面时，指令示例：

> "阅读 `claude.md`、`design.md` 和 `游寄_订单模块原型PRD.md`，制作订单看板原型页面 `order-dashboard.html`，严格遵守 claude.md，完成后按自检清单核对。"

---

**说明**：本文件为行为约束，视觉以 `design.md` 为准、内容以各 `PRD.md` 为准。三者分工不重叠，共同约束 Claude Code 产出一致、规范、可交付的高保真原型。