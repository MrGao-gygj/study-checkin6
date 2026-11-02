# 把「学习打卡」上传到 GitHub：手把手中文教程

> 目标：在 GitHub 上得到一个仓库 `https://github.com/你的用户名/study-checkin`，
> 里面包含 `index.html`、`package.json`、`render.yaml`、`server/server.mjs`。
> 全程不需要写代码、不需要买服务器，**10 分钟**左右。
>
> 传到 GitHub 只是第一步（存代码）；要让微信群里的人数据互通，还需要接着做
> `部署教程-发到微信群.md` 里的 Render + Gist（约 5 分钟）。

---

## 0. 上传前先认清「要传哪些，不要传哪些」

打开你电脑上的 `E:\together study - 副本\打卡工具` 文件夹，对照下表：

| 文件 / 文件夹 | 要不要传 | 说明 |
| --- | --- | --- |
| `index.html` | ✅ **必须** | 整个网页（单文件） |
| `package.json` | ✅ **必须** | 告诉 Render 怎么启动 |
| `render.yaml` | ✅ **必须** | Render 一键部署配置 |
| `server`（整个文件夹） | ✅ **必须** | 后端服务，里面是 `server/server.mjs`；**没有它数据无法共享** |
| `README.md` | 🔸 建议 | 项目说明，GitHub 首页会展示 |
| `启动打卡服务.cmd` | 🔸 可选 | Windows 本地启动脚本 |
| `学习打卡表.xlsx` | 🔸 可选 | 表格备份，不影响运行 |
| `预览/` 里的 PNG | ❌ 不用传 | 只是效果截图，会拖慢上传 |
| `checks.json`、`build_template.py`、`make_test_data.py`、`verify_test.py` | ❌ 不用传 | 生成/验证用的临时脚本 |
| `部署教程-发到微信群.md` | 🔸 可选 | 你自己看的教程 |

**最容易犯的错误**：只拖了 `index.html`。那样 GitHub 上只有一个静态页面，
没有后端 → 每个人打卡只存在自己手机里 → 就是「记录没同步」的典型原因。

---

## 1. 注册 / 登录 GitHub

1. 打开 https://github.com
2. 有账号：点右上角 **Sign in** 登录
3. 没账号：点 **Sign up** → 填邮箱、密码、用户名 → 收邮件点验证链接

> 用户名会出现在链接里（`github.com/用户名/...`），建议用英文/数字，好记。

---

## 2. 新建一个空仓库

1. 打开 https://github.com/new
2. 按下面填：

| 字段 | 填什么 |
| --- | --- |
| **Repository name** | `study-checkin`（可自定义，建议英文） |
| **Description** | 学习打卡：一天两次打卡 + 排行榜（可不填） |
| **Public / Private** | 选 **Public** 最省事；选 Private 也行（后面 Render 授权即可） |
| **Add a README file** | **不要勾**（我们有现成的 README，勾了反而多一次合并） |
| **Add .gitignore / license** | 都不用选 |

3. 点绿色按钮 **Create repository**

创建成功后会看到一个空仓库页面，中间有几行 "Quick setup" 提示——**先不用管它**，
下一步用网页上传。

---

## 3. 上传文件（三种方式，选一种）

### 方式 A：网页拖拽（最简单，推荐）

1. 在空仓库页面，点右侧 **Add file** 按钮 → 选 **Upload files**
2. 会看到 "Drag files here to add them to your repository" 的虚线框
3. 打开电脑上的 `打卡工具` 文件夹，**用鼠标框选**这 4 样一起拖进页面：
   - `index.html`
   - `package.json`
   - `render.yaml`
   - `server`（**整个文件夹**）
   - 想传 README 就再加 `README.md`
4. 松手后等文件列表出现（`server/server.mjs` 应该显示为 `server/server.mjs`，不是散开的 `server.mjs`）
5. 页面下方 **Commit changes** 区域，消息可以填：`上传学习打卡页面与后端`
6. 点 **Commit changes**（绿色按钮）

> 拖拽注意：
> - **拖文件夹本身**，不要先双击进 `server` 再拖里面的文件，否则目录结构会变平铺；
> - 浏览器用 Chrome / Edge 最稳（Firefox 新版也支持）；
> - 上传中不要关页面，等进度条走完再 Commit。

### 方式 B：GitHub Desktop（不想拖拽、以后要经常更新时更稳）

1. 下载安装 https://desktop.github.com ，打开后用 GitHub 账号登录
2. 回到第 2 步建好的仓库页面，复制仓库地址 `https://github.com/用户名/study-checkin.git`
3. GitHub Desktop → **File → Clone repository** → 选 **URL** 标签 → 粘贴地址 → **Clone**
   （选一个本地目录，例如 `D:\code`）
4. 打开克隆下来的文件夹，把 `index.html`、`package.json`、`render.yaml`、`server`、`README.md` 复制进去
5. 回到 GitHub Desktop：左侧会列出改动 → 左下角 Summary 填 `上传学习打卡页面与后端`
   → 点 **Commit to main** → 再点右上角 **Push origin**
6. 网页刷新仓库，能看到文件即成功

### 方式 C：命令行（电脑已装 Git 时最快）

在 `E:\together study - 副本\打卡工具` 文件夹里打开 PowerShell，依次执行：

```powershell
git init
git add index.html package.json render.yaml server README.md
git commit -m "上传学习打卡页面与后端"
git branch -M main
git remote add origin https://github.com/你的用户名/study-checkin.git
git push -u origin main
```

> 第一次 push 会弹窗要求登录：用浏览器授权，或填 GitHub 用户名 +
> Personal Access Token（Settings → Developer settings → Tokens，勾 `repo` 权限）。
> 如果提示 `remote origin already exists`，把 `git remote add` 换成
> `git remote set-url origin https://github.com/你的用户名/study-checkin.git`。

---

## 4. 传完必须验证这 3 点

1. 打开 `https://github.com/你的用户名/study-checkin`
2. 文件列表应该是：`index.html`、`package.json`、`render.yaml`、`server/`（可能还有 `README.md`）
3. **点进 `server` 文件夹**，里面必须有 `server.mjs`
   （如果文件列表里直接出现 `server.mjs` 而没有 `server` 文件夹，说明拖错了，见第 6 节）

再检查一下文件内容没坏：点 `index.html` → 右上角 **Raw** → 能看到 `<!DOCTYPE html>` 开头的源码。

> 这一步通过后，GitHub 就存好了。接着按 `部署教程-发到微信群.md` 的第 4–7 步
> 建 Gist、建 Token、在 Render 部署——**那一步才是让微信群共享数据的关键**。

---

## 5. 以后怎么更新（改完页面后）

**网页方式**：仓库 → **Add file → Upload files** → 重新拖入改过的文件
（比如只改了 `index.html` 就只拖它）→ **Commit changes**。
GitHub 会覆盖同名文件，并保留历史记录。

**Desktop 方式**：把新文件复制进本地仓库文件夹 → 打开 GitHub Desktop → Commit → Push。

**注意**：如果同时改了后端，记得 `server/server.mjs` 也要重新上传；只改前端则只需要 `index.html`。
传完 Render 会自动重新部署（约 1 分钟），不用手动操作。

---

## 6. 常见问题

| 问题 | 原因 | 怎么修 |
| --- | --- | --- |
| 上传后没有 `server` 文件夹，`server.mjs` 散在根目录 | 拖的是文件不是文件夹 | 删掉散落的 `server.mjs`（打开文件 → 右上角垃圾桶 → Commit），重新按方式 A 拖整个 `server` 文件夹 |
| 拖拽时浏览器把文件夹当成压缩包/没反应 | 浏览器不支持文件夹拖拽 | 改用方式 B（GitHub Desktop），或先上传文件、再手动建目录（Add file → Create new file，文件名写 `server/server.mjs` 再粘内容） |
| 点 **Commit changes** 没反应 / 按钮是灰的 | 还没选文件，或文件名重复未确认 | 确认虚线框里已有文件列表，再点绿色按钮 |
| 提示 "This file is too large" | 传了预览大图 | 只传代码文件，`预览/` 不需要上传 |
| 想传 Private 仓库 | 私有仓库同样能部署 | 建 Render 服务时给 GitHub App 授权访问该仓库即可 |
| 传错了想删 | — | 打开该文件 → 右上角 **垃圾桶图标** → Commit changes |
| 想把整个仓库删掉重来 | — | 仓库页 **Settings** → 最下面 **Danger Zone → Delete this repository**，输入仓库名确认 |

---

## 7. 传完后的检查清单

- [ ] 仓库里能看到 `index.html`
- [ ] 仓库里能看到 `package.json`
- [ ] 仓库里能看到 `render.yaml`
- [ ] 仓库里有 `server` 文件夹，点进去有 `server.mjs`
- [ ] `index.html` 点 Raw 能看到 HTML 源码
- [ ] 仓库是 Public，或已给 Render 授权（Private 时）
- [ ] 已按 `部署教程-发到微信群.md` 配好 Gist / Token / Render

全部打勾后，你就有了一个可部署的 GitHub 仓库。下一步（Gist + Token + Render）
照着另一份教程做即可；如果 Render 部署完打开页面右上角显示「已同步」，
说明整条链路通了。