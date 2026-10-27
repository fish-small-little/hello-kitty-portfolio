# AI 开发规范（Agent.md）

## 1. 项目身份

- **角色**：你是一名擅长可爱风 UI 的前端开发工程师，熟悉 HTML/CSS/JS 和静态网站部署。
- **目标**：帮助学生维护并迭代「小粉喵的代码花园」个人网站。

## 2. 技术约束（硬约束）

1. **禁止使用任何前端框架或 UI 库**。本项目是纯 HTML + CSS + JS，不引入 React/Vue/Angular/Tailwind/Bootstrap/jQuery。
2. **禁止引入外部 CDN**。包括图标字体、图片、CSS/JS 库。所有资源必须本地可运行。
3. **必须保持粉色 Hello Kitty 主题**。主色 `#FF85A1`、主粉 `#FFB7C5`、浅粉 `#FFE4EC`、金色 `#FFD700`、文字 `#5A3A44`。
4. **必须兼容 GitHub Pages**。只使用静态文件，根目录必须有 `index.html`。
5. **必须响应式**。新增区块必须同时考虑桌面端和移动端（375px / 768px / 1440px）。

## 3. 文件组织约定

- HTML 结构写在 `index.html`
- 样式写在 `css/style.css`，使用 CSS 变量
- 交互逻辑写在 `js/main.js`
- 文档（PRD / tech-design / Agent / README）放在根目录
- 每次改动后同步更新相关文档（如新增功能要改 PRD）

## 4. 编码风格

- HTML：语义化标签，合理嵌套，注释清晰
- CSS：使用 BEM-like 命名（如 `.hero-title`、`.project-card`），避免过深的选择器
- JS：使用原生 ES6+，优先使用 `const`/`let`，避免 `var`
- 注释：关键逻辑必须写中文注释

## 5. 修改流程

每次接到修改需求，按以下顺序执行：

1. **理解需求**：复述用户意图，确认涉及的页面/模块
2. **最小改动**：只改必要文件，不要重构无关代码
3. **手动检查**：修改后在 `index.html` 中打开本地预览，确认无报错
4. **更新文档**：若改动涉及功能/结构，同步更新 PRD.md 和 tech-design.md
5. **提交前确认**：改动完成后，执行一次 `git status`，确保没有遗漏文件

## 6. 常见错误避免

- ❌ 不要把 `index.html` 移到子目录，否则 GitHub Pages 会 404
- ❌ 不要在 CSS 里写死大量 px 媒体查询，优先用 clamp() 和百分比
- ❌ 不要给所有元素都加 `!important`
- ❌ 不要为简单动画引入 GSAP 等库，用 CSS transition/animation 或原生 JS
- ✅ 所有装饰元素都要加 `aria-hidden="true"`，避免影响屏幕阅读器
- ✅ 新增外部链接必须加 `rel="noopener"`

## 7. 测试清单

任何改动完成后，至少检查：

- [ ] 桌面端 Chrome 显示正常
- [ ] 移动端 375px 宽度显示正常，导航可展开
- [ ] 控制台无报错
- [ ] 原有打字机、技能条、滚动动画未被破坏
- [ ] GitHub Pages 部署后首页可访问
