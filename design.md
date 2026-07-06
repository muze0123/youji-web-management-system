# design.md — 视觉设计规范（单一事实来源）

> 本文件是项目视觉规范的**单一事实来源**，提取自《设计系统.html》。所有页面的颜色、字号、圆角、间距、组件外观**必须**引用本文件，不得自造。视觉如有调整，只改本文件。
> 配套文件：`claude.md`（工程与行为约束）、各模块 `PRD.md`（页面内容与交互）。

---

## 一、颜色

### 1.1 主色

| 角色 | 色值 | 用途 |
|------|------|------|
| primary | `#0066FF` | 主操作、选中、链接、品牌强调 |
| primary-hover | `#0052CC` | 主按钮 hover |
| primary-active | `#0047B3` | 主按钮 active |
| primary-bg | `#E6F0FF` | 主色浅底（选中背景、标签底） |

### 1.2 中性色（文字与线）

| 角色 | 色值 | 用途 |
|------|------|------|
| ink-title | `#1A1D24` | 标题文字 |
| ink-body | `#3A3F4A` | 正文 |
| ink-sub | `#6E7685` | 次要/辅助文字 |
| ink-muted | `#9DA2AC` | 占位/禁用文字 |
| line | `#DFE1E5` | 主分割线/边框 |
| line-light | `#E8EAED` | 浅分割线 |
| line-lighter | `#F0F1F3` | 更浅（表头底等） |
| bg-page | `#F7F8FA` | 页面底色 |
| bg-card | `#FFFFFF` | 卡片底色 |
| bg-hover | `#F3F4F6` | 行/项 hover 底色 |

### 1.3 语义色

| 角色 | 主色 | 浅底 | 用途 |
|------|------|------|------|
| success | `#0FC060` | `#E7F9F0` | 成功、进行中、完成正向 |
| warning | `#E7772D` | `#FDF2E9` | 警告、临期、超时提示 |
| danger | `#D9001B` | `#FFE8EB` | 错误、危险、异常、删除 |
| info | `#0091D5` | `#E4F4FB` | 信息、中性提示 |

### 1.4 语义色使用铁律

- 主操作/选中/链接 → **primary**
- 进行中/完成正向 → **success**
- 临期/超时/警告 → **warning**
- 异常/删除/错误 → **danger**
- 中性信息提示 → **info**
- 状态 Badge 一律"主色字/描边 + 对应浅底"

---

## 二、字体

### 2.1 字体族

| 用途 | 字体 |
|------|------|
| UI 文本（sans） | `-apple-system, BlinkMacSystemFont, 'PingFang SC', 'Microsoft YaHei', 'Hiragino Sans GB', 'Segoe UI', system-ui, sans-serif` |
| 数字/编号/金额/代码（mono） | `'JetBrains Mono', monospace` |

> 数字、订单号、金额、编码、时间戳等**必须**用 mono 字体，增强数据感与对齐。
> JetBrains Mono 通过 CDN 引入：`https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;500;600&display=swap`

### 2.2 字号层级（B 端高信息密度）

| 层级 | 字号 / 字重 | 用途 |
|------|-------------|------|
| 主标题 | 20–30px / 700 | 页面主标题 |
| 区块标题 | 16–19px / 600 | 卡片/区块标题 |
| 正文（主） | 13px / 400–500 | 表格、正文、表单 |
| 正文（次） | 12px / 400 | 密集信息 |
| 辅助 | 11px / 400 | 标签、次要说明 |

---

## 三、圆角与间距

### 3.1 圆角

| 值 | 用途 |
|----|------|
| **4px** | 默认（按钮、输入框、标签、小卡片） |
| 6px | 次选（卡片、弹窗） |
| 8px | 大容器 |

### 3.2 间距

- 基数 **6px**；
- 常用梯度：`4 / 6 / 8 / 10 / 12 / 16 / 20 / 32px`；
- 就近取梯度值，不用非梯度的随意像素。

---

## 四、阴影层次

| 层级 | 用途 | 参考 |
|------|------|------|
| 无/极浅 | 卡片默认（以边框区分为主） | `border: 1px solid line` |
| 轻 | hover 卡片、下拉 | `0 2px 8px rgba(0,0,0,.06)` |
| 中 | 弹窗、抽屉、悬浮层 | `0 6px 24px rgba(0,0,0,.12)` |

> B 端以边框和底色区分层级为主，阴影克制使用，避免过重。

---

## 五、组件外观标准

同类组件全站外观必须一致。以下为视觉标准（行为交互见 `claude.md`）。

### 5.1 按钮

| 类型 | 外观 |
|------|------|
| 主按钮 | primary 实底 + 白字，圆角 4px，高度 32px（默认）/28px（小） |
| 次按钮 | 白底 + line 描边 + ink-body 字 |
| 危险按钮 | danger 实底/描边 |
| 禁用 | 底色/文字置灰（ink-muted），不可点 |
| hover/active | 主按钮用 primary-hover / primary-active |

### 5.2 表格

| 区域 | 样式 |
|------|------|
| 表格整体 | `width:100%; border-collapse:collapse; font-size:13px` |
| 表头 | `line-lighter` 底色（`#F0F1F3`）+ `ink-sub` 字色（`#6E7685`），字重 600，字号 12px，padding `9px 12px`，下边框 `1px solid line`，不换行 |
| 数据行 | 字号 13px，`ink-body` 字色，padding `9px 12px`，下边框 `1px solid line-lighter`，行高约 44–52px |
| hover 行 | `bg-hover`（`#F3F4F6`）高亮底色；斑马纹可选 |
| 对齐 | **所有列左对齐**（含数字列）；列头与数据水平 padding 一致，保持上下对齐 |
| 数字列 | 使用 mono 字体（金额、数量、订单号等），与其他列保持左对齐 |
| 响应式 | 表格外层容器 `overflow-x: auto`，窄屏横向滚动 |
| 操作列 | 操作链接之间 12px 水平间距（如"编辑 删除"），危险操作（删除）用 danger 色 |

> **实现参考**：所有原型页面中表格使用 `.data-table` 类统一以上样式。新页面从框架模板复制后，表格 CSS 已内置。

### 5.3 状态 Badge

- 圆角标签（4px），主色字/描边 + 对应浅底；
- 进行中 success / 临期超时 warning / 异常 danger / 终态 ink-muted 灰。

### 5.4 筛选区

> 筛选区统一采用 4 列栅格布局，标签右对齐紧贴控件左侧，标签+控件宽度统一保证同行控件起始列对齐。

**容器 `.filter-grid`**：`display:grid; grid-template-columns:repeat(4,1fr); gap:10px 16px; align-items:start;`

- 响应式：≤1100px 降为 2 列、≤640px 降为 1 列。

**筛选行 `.filter-item`**：`display:flex; align-items:center; gap:0;`

**标签 `.filter-label`**：`width:78px; flex-shrink:0; text-align:right; font-size:14px; color:#1A1D24; line-height:32px; white-space:nowrap;`

- 标签末尾通过 `::after { content:'：'; }` 自动追加中文冒号；
- 标签区宽度统一（78px），保证同行 4 个字段的控件起始列对齐。

**控件 `.filter-ctrl`**：`flex:1; min-width:0;`

- 内部 `input` / `select`：`width:100%; height:32px; font-size:14px; padding:0 8px; border-radius:4px; border:1px solid #DFE1E5; color:#3A3F4A; outline:none; font-family:inherit; background:#fff;`
- placeholder 样式：`color:#9DA2AC; font-size:14px;`
- focus 态：`border-color:#0066FF; box-shadow:0 0 0 2px rgba(0,102,255,.12);`
- select 下拉箭头使用内联 SVG background-image 替代浏览器默认样式，`padding-right:24px;`

**日期范围 `.date-range`**：`display:flex; align-items:center; gap:4px;`

- 分隔符 `.date-sep`：`font-size:14px; color:#9DA2AC; flex-shrink:0; margin:0 2px;`
- 日期输入框使用 `type="text"` + `placeholder` 展示提示文字，focus 时切换 `type="date"` 调用原生日期选择器，blur 无值时恢复 `type="text"` 显示 placeholder。
- 空状态文字色 `#9DA2AC`，有值后切换为 `#3A3F4A`。

**查询/重置按钮**放在筛选区末列（使用 `visibility:hidden` 的占位标签对齐），按钮高度 32px 与控件一致。

**筛选字段顺序建议**：搜索框放第一位，日期范围合并为一个字段（`创建时间：[开始时间 - 结束时间]`），其余按业务优先级排列。一行 4 个字段，超出 4 个自动换行。

**搜索框清空按钮**：搜索输入框在有内容时，右侧显示清空按钮 `✕`（位于搜索图标对面），点击后清空输入内容并保持焦点；无内容时按钮隐藏。清空按钮样式：`position:absolute;right:8px;top:50%;transform:translateY(-50%);width:16px;height:16px;font-size:12px;color:#9DA2AC;cursor:pointer`，hover 时颜色变深 `#6E7685`。

### 5.5 分页

> 严格对齐设计系统.html 中的分页器组件。

**容器**：`display:flex;align-items:center;justify-content:flex-end;flex-wrap:wrap;gap:16px;font-size:12px`。

**位置**：分页器放在数据表格所在区块卡片（`.bg-white.rounded-lg.border`）内部，位于表格（`.overflow-x-auto`）的右下方，通过 `pt-5`（20px）与上方表格区域保持间距。分页器**不是**独立的区块卡片，而应与表格同属一个卡片区块。

**布局（三区，居右）**：

| 位置 | 内容 | 说明 |
|------|------|------|
| 左 | 页码导航 `#pg-nav` | `display:flex;gap:4px` — `‹` + 页码按钮 + 省略号 `…` + `›` |
| 中 | 条/页选择 | `.pg-select-wrap` 包裹 `<select>`，`::after` 自定义下拉箭头 |
| 右 | 跳页 + 统计 | 跳至 `[input]` 页 + `共 N 条记录　第 a/b 页` |

**页码按钮 `.pg-btn`**：`min-width:30px;height:30px;padding:0 8px;font:500 12px inherit;color:#3A3F4A;background:#fff;border:1px solid #DFE1E5;border-radius:4px;cursor:pointer;transition:all .15s;display:inline-flex;align-items:center;justify-content:center`
- hover（非当前页、非禁用）：`color:primary;border-color:primary`
- 当前页 `.pg-current`：`background:primary;border-color:primary;color:#fff`
- 禁用（首页 `‹` / 末页 `›`）：`color:#C7CAD1;background:#F7F8FA;cursor:not-allowed;border-color:#DFE1E5`

**省略号 `.pg-ellipsis`**：`min-width:30px;height:30px;display:inline-flex;align-items:center;justify-content:center;color:#9DA2AC;font-size:13px`

**条/页下拉 `.pg-select`**：`font:12px inherit;height:30px;padding:0 28px 0 8px;border-radius:4px;border:1px solid #DFE1E5;color:#3A3F4A;background:#fff;cursor:pointer;appearance:none;-webkit-appearance:none`
- `.pg-select-wrap`：`position:relative;display:inline-flex;align-items:center`
- `.pg-select-wrap::after`：`content:'▼';position:absolute;right:8px;font-size:8px;color:#9DA2AC;pointer-events:none`

**跳页输入框 `.pg-jump-input`**：`font:12px inherit;width:44px;height:30px;text-align:center;border-radius:4px;border:1px solid #DFE1E5;color:#3A3F4A;outline:none`
- focus：`border-color:primary;box-shadow:0 0 0 2px rgba(0,102,255,.12)`

**统计文字 `.pg-stats`**：`color:#9DA2AC;white-space:nowrap`

**页码逻辑**：≤7 页全显示；>7 页时始终显示首页和末页，当前页 ±1 范围显示，其余用 `…` 折叠。

### 5.6 弹窗 Modal

- 居中；遮罩 `rgba(0,0,0,.3)`；圆角 8px；宽度 **760px**（`max-width:92vw` 响应式）；
- 结构：标题栏（16px/600）+ 关闭 ×（20px，ink-muted，右上角）+ 内容区（padding 32px 24px）+ 底部操作区（border-top 分隔，按钮居右）；
- 表单字段：label 90px 右对齐（标签文字末尾带中文冒号 `：`）+ 控件 400px 宽 30px 高（`border-radius:4px;border:1px solid line`）；字段区块在弹窗内容区居中。

### 5.7 抽屉 Drawer

- 右侧滑出；用于详情展示；宽度 **800px**（`max-width:100%` 响应式）；
- 遮罩 `rgba(0,0,0,.3)`；阴影 `-4px 0 24px rgba(0,0,0,.1)`；入场动画 `ds-drawer-in .22s ease`；
- 结构：标题栏（16px/600 + 关闭 ×）+ 内容区（`overflow-y:auto`）+ 底部按钮。

### 5.8 信息提示弹窗 Dialog

> 严格对齐设计系统.html 中的 Dialog 组件。用于信息提示、操作确认（如删除确认）等轻量场景，与 Modal（表单弹窗）区分。

**容器**：`position:fixed;inset:0;background:rgba(0,0,0,.3);z-index:1200;display:flex;align-items:center;justify-content:center`

**弹窗本体**：`width:600px;max-width:92vw;height:250px;background:#fff;border-radius:8px;box-shadow:0 8px 32px rgba(0,0,0,.12);display:flex;flex-direction:column;position:relative;animation:ds-modal-in .15s ease`

**结构**：

| 区域 | 样式 |
|------|------|
| 关闭 × | `position:absolute;top:14px;right:18px;font-size:20px;color:#9DA2AC;cursor:pointer;z-index:1`（纯文本 `×`，非 Lucide 图标） |
| 内容区 | `flex:1;display:flex;align-items:center;padding:0 24px` |
| ICO | `width:20px;height:20px;border-radius:50%;flex-shrink:0` 圆形图标，颜色随 Dialog 类型变化 |
| 标题 | `font-size:16px;font-weight:600;color:#1A1D24` |
| 副标题 | `font-size:14px;color:#6E7685;margin-top:6px` |
| 底部按钮区 | `padding:0 24px 20px;display:flex;justify-content:flex-end;gap:12px` |
| 取消按钮 | `font:500 13px inherit;padding:6px 20px;border-radius:4px;background:#fff;color:#3A3F4A;border:1px solid #DFE1E5;cursor:pointer` |
| 确定按钮 | `font:500 13px inherit;padding:6px 20px;border-radius:4px;border:1px solid transparent;cursor:pointer;background:primary;color:#fff` |

**6 种 Dialog 类型**：

| 类型 | ICO | 图标色 | 底色 | 用途 |
|------|-----|--------|------|------|
| info | `i` | `#0091D5` | `#E4F4FB` | 信息提示 |
| success | `✓` | `#0FC060` | `#E7F9F0` | 操作成功 |
| warning | `!` | `#E7772D` | `#FDF2E9` | 警告提示 |
| danger | `✕` | `#D9001B` | `#FFE8EB` | 错误提示（操作失败、系统异常等已发生的错误） |
| confirm | `?` | `#E7772D` | `#FDF2E9` | 操作确认（删除确认、标记异常等需用户二次确认的操作） |

> **删除确认**使用 `confirm` 类型（ICO `?`），因为本质是"确认是否执行"的询问，而非已发生的错误。确定按钮可使用 `danger` 红底强调破坏性操作。
| system | `ⓘ` | `#0091D5` | `#E4F4FB` | 系统通知 |

### 5.9 表单

- label（标签文字末尾带中文冒号 `：`）+ 控件；必填标识 `*`（danger 色）位于标签文字**左侧**（即 `* 字段名：`）；
- 控件默认宽度 400px、高度 30px（输入框/下拉框）；圆角 4px；边框 1px solid line；
- 校验错误：控件描边转 danger + 下方 danger 字提示。

**字符计数器 `x/y`**（全局适用）：

| 控件类型 | 计数器位置 | 说明 |
|---------|-----------|------|
| 单行文本输入框 `<input>` | 控件内**右侧** | `x` 为当前已输入字符数，`y` 为最大字符数（`maxlength`），输入时实时更新 |
| 多行文本域 `<textarea>` | 控件外**右下侧** | 同上，位于文本域下方、右对齐 |

- 计数器样式：字号 12px，颜色 `ink-muted`（`#9DA2AC`），格式 `x/y`（如 `0/20`、`15/200`）；
- 单行输入框：计数器 `position:absolute` 定位在输入框内右侧，输入框 `padding-right` 预留 48px 空间，避免输入文字与计数器重叠；
- 多行文本域：计数器独立一行，`text-align:right`，宽度与文本域一致；
- 计数逻辑：以 `input.value.length` 为准，maxlength 由 `input` 属性直接提供或隐式声明。

**Toggle 开关**：

- 尺寸 40×22px，圆角 11px；圆钮 18px 白色；过渡 `.2s`；
- 关闭态：底色 `#C7CAD1`，圆钮居左（`left:2px`）；
- **开启态：底色 primary `#0066FF`**（非 success 绿），圆钮居右（`translateX(18px)`）。

### 5.10 卡片

- `bg-card` + `line` 边框 + 圆角 6px + 内边距 16–20px。

### 5.11 图标

- Lucide 图标；尺寸随文本（14–16px 常用）；颜色随语义。

### 5.12 空状态 / 加载态

- 空状态：图标 + 说明文案 +（可选）操作引导；
- 加载态：骨架屏或 loading 指示。

### 5.13 交互标注徽标（Portal 图层）

> 标注徽标通过 Portal 独立图层渲染，与页面 DOM 完全解耦。详见 `claude.md` §7。

| 属性 | 值 |
|------|----|
| 尺寸 | 20×20px 圆形 |
| 底色 | primary `#0066FF` |
| 文字 | 白色，11px，700 |
| 阴影 | `0 2px 6px rgba(0,0,0,.15)` |
| z-index | 9998（图层）/ 9999（弹窗） |
| hover | `transform: scale(1.2)` |
| 定位 | `position: fixed`，动态计算目标元素右上角坐标（`rect.top - 10`, `rect.right - 10`） |

---

## 六、布局规范

### 6.1 后台（Web 管理系统）

经典三段布局：

```
顶部栏 TopBar（系统名 / 用户 / 退出）
├─ 侧边导航 Sidebar（220px，可折叠，当前页高亮）
│   ├─ 一级菜单 .menu-item.l1：padding-left 20px，含 28×28 图标 + 10px 间距，文字起始 58px
│   └─ 二级菜单 .menu-item.l2：padding-left 64px（比一级文字右缩 6px，形成层级缩进）
└─ 主内容区 MainContent（flex-1，bg-page 背景，p-4 内边距，自适应宽度）
    ├─ 内容卡片：bg-white rounded-lg border p-5 md:p-6
    ├─ 单区块：卡片最小高度 = 内容区高度 − 16px（`min-h-full` + `flex-1` 撑满），内容超过时自适应增高，main 滚动
    ├─ 多区块（≥2）：卡片高度由内容决定，垂直堆叠，间距 16px（mb-4）
    └─ 无面包屑，页面标题内嵌于首张卡片中
```

### 6.2 用户端（小程序，如需）

- 移动端竖屏基准宽 375px；页面中居中放"手机外框"容器展示；主色仍用本规范 token。

---

## 七、Tailwind 配置镜像（供实现直接引用）

> 以下为本规范的 Tailwind 映射，实现时内联到页面 `tailwind.config`。**本文件为准，此为镜像。**

```js
tailwind.config = {
  theme: {
    extend: {
      colors: {
        primary: { DEFAULT: '#0066FF', hover: '#0052CC', active: '#0047B3', bg: '#E6F0FF' },
        ink:     { title: '#1A1D24', body: '#3A3F4A', sub: '#6E7685', muted: '#9DA2AC' },
        line:    { DEFAULT: '#DFE1E5', light: '#E8EAED', lighter: '#F0F1F3' },
        bg:      { page: '#F7F8FA', card: '#FFFFFF', hover: '#F3F4F6' },
        success: { DEFAULT: '#0FC060', bg: '#E7F9F0' },
        warning: { DEFAULT: '#E7772D', bg: '#FDF2E9' },
        danger:  { DEFAULT: '#D9001B', bg: '#FFE8EB' },
        info:    { DEFAULT: '#0091D5', bg: '#E4F4FB' },
      },
      borderRadius: { DEFAULT: '4px', md: '6px', lg: '8px' },
      fontFamily: {
        sans: ['-apple-system','BlinkMacSystemFont','PingFang SC','Microsoft YaHei','Hiragino Sans GB','Segoe UI','system-ui','sans-serif'],
        mono: ['JetBrains Mono','monospace'],
      },
    }
  }
}
```

---

**说明**：本文件与《设计系统.html》保持一致。若设计系统更新，先更新《设计系统.html》，再同步本文件，确保单一事实来源。