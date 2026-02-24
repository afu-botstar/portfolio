# 把网站托管到 GitHub Pages 详细步骤

## 一、事前准备

### 1. 安装 Git（如果还没装）

- **Windows**：到 [https://git-scm.com/download/win](https://git-scm.com/download/win) 下载安装包，按默认选项安装即可。
- 安装完成后，在任意文件夹空白处右键，能看到 **“Git Bash Here”** 或 **“在终端中打开”** 就说明装好了。

### 2. 注册 / 登录 GitHub

- 打开 [https://github.com](https://github.com)，注册或登录账号。
- 记下你的 **用户名**（例如 `afu-botstar`），后面会用到。

### 3. 确认项目文件夹里要有这些内容

网站能正常打开至少需要：

- `index.html`（必须）
- `front/` 文件夹（3 个字体文件）
- `article/` 文件夹（Design 页的封面和正文图）
- `AI/` 文件夹（Tool 页图标 `icon128.webp`）
- 根目录图片：`bg-card.webp`、`home-me_1.webp`～`home-me_6.webp`、`avatar1.webp`、所有 `work*.webp`、`jike.webp`、`wechat.webp`、`xiaohongshu.webp`

少哪个，线上对应位置就会裂图或缺样式。

---

## 二、在 GitHub 上新建仓库

1. 登录 GitHub，右上角点击 **“+”** → **“New repository”**。
2. 填写信息：
   - **Repository name**：起一个英文名，例如 `portfolio` 或 `my-website`。  
     - 若用 `用户名.github.io` 当仓库名，最后访问地址会是 `https://用户名.github.io/`（没有仓库名路径）。
   - **Description**：可选，例如“个人作品集”。
   - **Public** 选上。
   - **不要**勾选 “Add a README file”“Add .gitignore”“Choose a license”（你本地已有完整项目）。
3. 点击 **“Create repository”**。
4. 创建完成后，页面上会有一个仓库地址，形如：  
   `https://github.com/你的用户名/仓库名.git`  
   复制保存，后面会用到。

---

## 三、在本地用 Git 把项目推上去

### 方式 A：用 Cursor / VS Code 自带终端

1. 在 Cursor 里打开项目文件夹（确保是包含 `index.html` 的那一层）。
2. 按 **Ctrl + `** 打开底部终端（或菜单 **终端 → 新建终端**）。
3. 确认当前路径是项目根目录，然后按顺序执行下面命令（一行一行执行，每行回车一次）。

### 第一步：初始化 Git 仓库

```bash
git init
```

- 说明：在当前文件夹里创建一个“.git”目录，表示这里是一个 Git 项目。只需做一次。

### 第二步：把文件加入“暂存区”

```bash
git add .
```

- 说明：`.` 表示当前目录下所有文件（遵守 `.gitignore` 规则）。所有要上传的文件会被标记为“待提交”。

### 第三步：做第一次提交

```bash
git commit -m "Initial commit: portfolio site"
```

- 说明：把暂存区里的内容打成一次“提交”，`-m` 后面是这次提交的说明，可以改成任意中文或英文。

### 第四步：把默认分支命名为 main（推荐）

```bash
git branch -M main
```

- 说明：GitHub 现在默认主分支叫 `main`，这样后面和 GitHub Pages 设置一致。

### 第五步：把本地仓库和 GitHub 上的仓库连起来

```bash
git remote add origin https://github.com/你的用户名/仓库名.git
```

- **重要**：把 `你的用户名` 和 `仓库名` 换成你第二步里创建仓库时用的。  
  例如：`git remote add origin https://github.com/afu-botstar/portfolio.git`
- 说明：`origin` 是远程仓库的默认名字，以后 `git push` 就会推送到这个地址。

### 第六步：推送到 GitHub

```bash
git push -u origin main
```

- 说明：把本地的 `main` 分支推送到 GitHub；`-u` 表示以后在这个分支上可以直接用 `git push`，不用再写 `origin main`。
- 第一次推送时，可能会弹出浏览器或提示你登录 GitHub：
  - 若要求输入 **用户名** 和 **密码**：密码处要填 **Personal Access Token**，不是登录密码。  
    - 生成 Token：GitHub 右上角头像 → **Settings** → 左侧最下面 **Developer settings** → **Personal access tokens** → **Tokens (classic)** → **Generate new token**，勾选 `repo`，生成后复制保存，在命令行里当密码粘贴。
  - 若使用 **Git Credential Manager** 或 **GitHub Desktop**，按提示在浏览器里登录即可。

全部执行完后，刷新你的 GitHub 仓库页面，应该能看到所有文件都已经在仓库里。

---

## 四、开启 GitHub Pages（让网站被访问）

1. 在 GitHub 上打开你的仓库（不是个人主页）。
2. 点击顶部的 **“Settings”**（设置）。
3. 左侧菜单找到 **“Pages”**（在 **Code and automation** 下面），点进去。
4. 在 **“Build and deployment”** 里：
   - **Source** 选 **“Deploy from a branch”**（从分支部署）。
   - **Branch** 选 **“main”**，右边文件夹选 **“/ (root)”**。
   - 点 **“Save”** 保存。
5. 等 1～2 分钟，页面上方会出现一条绿色提示，写着你网站的地址，形如：  
   **Your site is live at https://用户名.github.io/仓库名/**  
   例如：`https://afu-botstar.github.io/portfolio/`
6. 用浏览器打开这个地址，就能看到你托管的网站。

---

## 五、访问地址的两种常见情况

| 仓库名 | 访问地址 |
|--------|----------|
| 普通名字，如 `portfolio` | `https://你的用户名.github.io/portfolio/` |
| 特殊名字：`你的用户名.github.io` | `https://你的用户名.github.io/`（根路径就是网站） |

注意：除了 `用户名.github.io` 这种仓库，其它仓库的 Pages 地址最后都带一层 **仓库名**，例如 `/portfolio/`，不能少。

---

## 六、以后怎么更新网站

每次改完 `index.html` 或图片、字体等资源后：

1. 在项目文件夹里打开终端（同上）。
2. 依次执行：

```bash
git add .
git commit -m "这里写你这次改了什么，比如：更新首页文案"
git push
```

3. 推送成功后，等 1～3 分钟，再刷新你的 GitHub Pages 地址，就能看到更新。

---

## 七、常见问题

### 1. 提示 “git 不是内部或外部命令”

- 说明本机还没装 Git，或安装后没重启终端。先安装 Git（见“一、事前准备”），关闭再打开终端后重试。

### 2. 推送时提示 “Permission denied” 或 “Authentication failed”

- 说明 GitHub 认证没过：  
  - 若用账号密码，密码必须用 **Personal Access Token**；  
  - 或使用 GitHub Desktop、Git Credential Manager 通过浏览器登录一次。

### 3. 打开 Pages 地址是 404

- 检查：Settings → Pages 里是否选了 **main** 分支和 **/ (root)**。  
- 确认 `index.html` 在仓库**根目录**（不能在一个子文件夹里）。  
- 再等几分钟，Pages 部署有延迟。

### 4. 页面能打开但图片/字体不显示

- 说明引用路径和仓库里的文件不一致。  
- 检查：仓库里的文件夹名、文件名是否和 `index.html` 里写的一致（大小写、空格、中文都要一致）。  
- 图片路径是相对路径，例如 `article/article_1.webp`，表示根目录下的 `article` 文件夹里的 `article_1.webp`。

### 5. 想用自己买的域名

- 在域名服务商那里添加一条 **CNAME 记录**，指向 `你的用户名.github.io`（不用写仓库名）。  
- 在仓库 Settings → Pages 的 **Custom domain** 里填你的域名，保存。  
- 若 GitHub 提示 **Enforce HTTPS**，勾选上即可。

---

## 八、小结：你要做的顺序

1. 装 Git，有 GitHub 账号。  
2. 在 GitHub 上 **New repository**，得到仓库地址。  
3. 在项目文件夹终端里：`git init` → `git add .` → `git commit -m "..."` → `git branch -M main` → `git remote add origin 仓库地址` → `git push -u origin main`。  
4. 仓库 **Settings → Pages**，选 **main** 和 **/ (root)**，保存。  
5. 用提示的 **https://用户名.github.io/仓库名/** 访问网站。  
6. 以后改完代码就：`git add .` → `git commit -m "更新说明"` → `git push`。

按这个流程做一遍，你的网站就会稳定挂在 GitHub 上，并且可以随时用 `git push` 更新。

---

## 九、加载更快 + 给国内面试官的访问建议

### 已做的加载优化

- 图片已改为 WebP，体积更小。
- 首屏两张图（`bg-card.webp`、`home-me_1.webp`）已做 **preload** 和 **fetchpriority="high"**，首屏会更快。
- 其余图片使用 `loading="lazy"`，滚动到时再加载。

### 若发给国内面试官：建议多一个国内可访问的链接

- **GitHub / GitHub Pages** 在国内有时较慢或被限制，面试官可能打不开或等很久。
- **建议**：同一份项目再部署一份到国内或国际 CDN，发简历时给两个链接：
  - **主链接（国内优先）**：下面任选一个，国内访问通常更稳定。
  - **备用链接**：`https://你的用户名.github.io/portfolio/`（GitHub Pages）。

**国内 / 国际访问都较稳的免费部署方式：**

| 方式 | 说明 | 国内访问 |
|------|------|----------|
| **Gitee 码云 Pages** | 和 GitHub 类似，把仓库推到 Gitee，开启 Gitee Pages | 一般较快 |
| **Vercel** | 用 GitHub 仓库一键导入，自动部署，带 CDN | 多数情况可用 |
| **Netlify** | 同上，连 GitHub 后自动部署 | 多数情况可用 |

发简历时可以写：「作品集：https://xxx（主链接），备用：https://用户名.github.io/portfolio/」。
