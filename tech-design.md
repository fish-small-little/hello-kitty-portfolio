# 技术设计文档

## 1. 技术栈

| 层级 | 技术 | 说明 |
|---|---|---|
| 结构 | HTML5 | 语义化标签，单页结构 |
| 样式 | CSS3 | 原生 CSS 变量、Flexbox、Grid、媒体查询 |
| 交互 | 原生 JavaScript | 无框架，减少依赖 |
| 部署 | GitHub Pages | 静态托管，自动从 main 分支根目录部署 |

**不使用的技术**：
- 无 React / Vue / Angular（项目简单，不需要组件化）
- 无 Tailwind / Bootstrap（为展示手写 CSS 能力）
- 无 jQuery（现代浏览器原生 API 已足够）
- 无后端服务 / 数据库（纯静态）

## 2. 文件结构

```
hello-kitty-portfolio/
├── index.html          # 单页入口
├── css/
│   └── style.css       # 全部样式
├── js/
│   └── main.js         # 交互逻辑
├── PRD.md              # 产品需求文档
├── tech-design.md      # 本文件
├── Agent.md            # AI 开发规范
└── README.md           # 部署与使用说明
```

## 3. 关键设计决策

### 3.1 为什么用单页而非多页？
- 内容量不大，单页可以通过锚点平滑滚动
- 减少 HTTP 请求，GitHub Pages 加载更快
- 便于实现统一的导航和页脚

### 3.2 为什么不用外部图标字体？
- 减少外部依赖，避免国内网络加载失败导致图标缺失
- 使用 SVG 内联绘制头像和 logo，保证清晰度
- 装饰元素使用 Unicode emoji（🎀🐾💖），兼容性好

### 3.3 响应式断点

| 断点 | 布局变化 |
|---|---|
| ≥ 1120px | 最大内容宽度 1120px，居中 |
| 900px | 项目/关于/联系卡片从三列变为单列；Hero 改为上下布局 |
| 640px | 导航折叠为汉堡菜单；内边距减小 |

## 4. CSS 设计系统

### 4.1 颜色变量

```css
--primary: #FF85A1;          /* 深粉，用于按钮、强调 */
--primary-dark: #FF5C85;     /* 更深的粉，用于 hover */
--primary-light: #FFB7C5;    /* 主粉，用于装饰、标签 */
--primary-lighter: #FFE4EC;  /* 浅粉，用于背景 */
--primary-soft: #FFF0F5;     /* 更浅的页面背景 */
--accent: #FFD700;           /* 金色，蝴蝶结、高亮下划线 */
--text: #5A3A44;             /* 主文字 */
--text-light: #8A6A74;       /* 次要文字 */
--white: #FFFFFF;
```

### 4.2 圆角与阴影

- 大卡片圆角：`24px`
- 小标签/按钮圆角：`50px`
- 默认阴影：`0 10px 30px rgba(255, 133, 161, 0.15)`
- 悬停阴影：`0 16px 40px rgba(255, 133, 161, 0.25)`

### 4.3 字体栈

```css
font-family: "PingFang SC", "Microsoft YaHei", "Hiragino Sans GB", "Helvetica Neue", Arial, sans-serif;
```

使用系统字体，避免加载外部字体文件。

## 5. 关键实现细节

### 5.1 打字机效果

- 使用一个文本数组循环
- 每个字符逐字显示，显示完整后停顿 1.8 秒
- 然后逐字删除，删除后切换下一条
- 使用 `setTimeout` 控制节奏，不使用 CSS 动画

### 5.2 滚动显示动画

- 使用 `IntersectionObserver` 监听 `.card-reveal` 元素
- 当元素 12% 进入视口时，添加 `.visible` 类
- `.visible` 类将元素从 `opacity: 0; transform: translateY(30px)` 变为完全显示
- 每个元素只触发一次

### 5.3 技能条动画

- 初始宽度为 0
- 当「关于我」区块进入视口时，读取 `data-width` 属性
- 通过 `transition` 将宽度从 0 动画到目标百分比
- 使用 `cubic-bezier(0.22, 1, 0.36, 1)` 缓动，呈现弹性效果

### 5.4 移动端菜单

- 默认 `.nav-links` 在桌面端横向排列
- 在 ≤ 640px 时，通过 `transform: translateY(-150%)` 隐藏菜单
- 点击汉堡按钮切换 `.open` 类，菜单滑入
- 点击任意导航链接后自动关闭菜单

## 6. 性能优化

- 无图片资源，全部使用 CSS/SVG/Unicode，减少请求
- CSS 和 JS 文件体积小（CSS ~9KB，JS ~3KB）
- 使用 `scroll-behavior: smooth` 替代 JS 平滑滚动
- 使用 CSS 变量统一管理主题色，便于维护和修改

## 7. 安全考虑

- 所有外部链接使用 `target="_blank" rel="noopener"`，防止标签页通过 `window.opener` 操纵原页面
- 不引入第三方 CDN，避免 XSS 和隐私泄露风险
- 无用户输入表单，无 SQL 注入 / XSS 攻击面

## 8. 扩展性

- 新增项目：在 `index.html` 的 `.project-grid` 中复制一个 `.project-card`
- 新增日志：在 `.log-list` 中复制一个 `.log-card`
- 修改主题色：只需改 `:root` 中的 CSS 变量
- 新增页面区块：在 `index.html` 中按 `.section` 结构添加，CSS 自动继承响应式
