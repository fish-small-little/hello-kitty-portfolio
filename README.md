# 小粉喵的代码花园 · 个人网站

一个粉色 Hello Kitty 主题的学生个人作品集网站，纯 HTML/CSS/JS 开发，部署于 GitHub Pages。

## 项目内容

- **PRD.md**：产品需求文档
- **tech-design.md**：技术设计文档
- **Agent.md**：AI 开发规范
- **index.html**：网站首页
- **css/style.css**：样式文件
- **js/main.js**：交互脚本

## 本地预览

1. 解压 `hello-kitty-portfolio.zip`
2. 双击 `index.html`，用浏览器打开即可

或者使用本地服务器（推荐）：

```bash
# 进入项目目录
cd hello-kitty-portfolio

# 用 Python 启动本地服务器
python -m http.server 8080

# 浏览器打开 http://localhost:8080
```

## 部署到 GitHub Pages（推荐）

### 第 1 步：在 GitHub 新建仓库

1. 打开 https://github.com/new
2. Repository name 填 `hello-kitty-portfolio`
3. 选择 **Public**
4. **不要勾选** "Add a README file"（本仓库已有 README）
5. 点击 **Create repository**

### 第 2 步：本地初始化并推送

在项目文件夹里打开 Git Bash（或 VS Code 终端），依次执行：

```bash
# 配置你的 Git 身份（如果还没配置过）
git config --global user.name "你的名字"
git config --global user.email "你的GitHub邮箱"

# 初始化仓库
git init

# 添加所有文件
git add .

# 提交
git commit -m "feat: 初始化粉色 Hello Kitty 个人网站"

# 绑定远程仓库（把 你的用户名 换成你的 GitHub 用户名）
git remote add origin https://github.com/你的用户名/hello-kitty-portfolio.git

# 推送到 main 分支
git branch -M main
git push -u origin main
```

第一次推送会弹出 GitHub 登录窗口，点 "Sign in with your browser" 完成授权即可。

### 第 3 步：开启 GitHub Pages

1. 进入仓库页面：https://github.com/你的用户名/hello-kitty-portfolio
2. 点击顶部 **Settings**
3. 左侧菜单找到 **Pages**
4. Source 选择 **Deploy from a branch**
5. Branch 选择 **main**，目录选择 **/ (root)**
6. 点击 **Save**
7. 等待 1–2 分钟，页面顶部会出现绿色提示：

```
Your site is live at https://你的用户名.github.io/hello-kitty-portfolio/
```

这就是你的个人网站域名。

### 第 4 步：验证

用浏览器的**无痕窗口**打开上面的域名，确认：

- 首页打字机效果正常
- 滚动到「关于我」时技能条有动画
- 项目卡片、实训日志、联系方式都显示正常
- 移动端宽度下导航能折叠

## 部署到 Netlify（备选）

如果 GitHub Pages 访问较慢，可以用 Netlify Drop：

1. 打开 https://app.netlify.com/drop
2. 把整个 `hello-kitty-portfolio` 文件夹拖进去
3. 等待 10 秒左右
4. 得到类似 `https://xxxx.netlify.app` 的域名

## 个性化修改

### 修改个人信息

打开 `index.html`，搜索并替换以下内容：

- `小粉喵` → 你的名字
- `hello@example.com` → 你的邮箱
- `fish-small-little` → 你的 GitHub 用户名
- `xiaofenmiao_code` → 你的微信号

### 修改主题色

打开 `css/style.css`，修改 `:root` 里的 CSS 变量：

```css
:root {
    --primary: #FF85A1;        /* 深粉 */
    --primary-light: #FFB7C5;  /* 主粉 */
    --primary-lighter: #FFE4EC; /* 浅粉 */
    --accent: #FFD700;          /* 金色 */
    --text: #5A3A44;            /* 文字色 */
}
```

### 添加新项目

在 `index.html` 的 `.project-grid` 中复制一个 `.project-card`，修改标题、描述、标签和链接即可。

### 添加新日志

在 `index.html` 的 `.log-list` 中复制一个 `.log-card`，修改日期、标题、摘要和标签即可。

## 常见问题

**Q：GitHub Pages 打开是 404？**

A：检查以下三点：
1. 仓库是 Public
2. Pages 设置中 Branch 选的是 `main`，目录是 `/ (root)`
3. 仓库根目录下存在 `index.html`

**Q：推送时提示 `fatal: not a git repository`？**

A：说明当前目录没有初始化 Git，先执行 `git init`。

**Q：修改后网页没有更新？**

A：GitHub Pages 有缓存，修改后等 1–3 分钟再刷新；或者按 `Ctrl+F5` 强制刷新。

**Q：怎么截图给老师？**

A：
- 桌面端：按 `Win + Shift + S` 截整个浏览器窗口，地址栏要可见
- 移动端：按 F12 打开开发者工具，切换到手机视图，截一张竖屏效果
