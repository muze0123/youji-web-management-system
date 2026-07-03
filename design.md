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

- 表头：`line-lighter` 底 + `ink-sub` 字，字号 12–13px；
- 行：高度舒适（约 44–52px），`line-light` 分隔；
- hover 行：`bg-hover` 高亮；斑马纹可选；
- 数字列用 mono 字体、右对齐（金额、数量）。

### 5.3 状态 Badge

- 圆角标签（4px），主色字/描边 + 对应浅底；
- 进行中 success / 临期超时 warning / 异常 danger / 终态 ink-muted 灰。

### 5.4 筛选区

- 下拉、日期范围、搜索框横向排列；右侧"查询/重置"按钮；控件高度与按钮一致（32px）。

### 5.5 分页

- 右下角；含总数、页码、每页条数选择。

### 5.6 弹窗 Modal

- 居中；遮罩 `rgba(0,0,0,.45)`；圆角 6px；含标题 / 内容 / 底部操作区。

### 5.7 抽屉 Drawer

- 右侧滑出；用于详情展示；宽度 480–560px。

### 5.8 表单

- label + 控件；必填标 `*`（danger 色）；
- 校验错误：控件描边转 danger + 下方 danger 字提示。

### 5.9 卡片

- `bg-card` + `line` 边框 + 圆角 6px + 内边距 16–20px。

### 5.10 图标

- Lucide 图标；尺寸随文本（14–16px 常用）；颜色随语义。

### 5.11 空状态 / 加载态

- 空状态：图标 + 说明文案 +（可选）操作引导；
- 加载态：骨架屏或 loading 指示。

---

## 六、布局规范

### 6.1 后台（Web 管理系统）

经典三段布局：

```
顶部栏 TopBar（系统名 / 用户 / 退出）
├─ 侧边导航 Sidebar（200–240px，可折叠，当前页高亮）
└─ 主内容区 MainContent（面包屑 + 标题 + 操作栏 + 筛选 + 数据区 + 分页）
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