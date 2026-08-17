# 交接说明｜一步一步六年级学习网页

## 项目目标

这是一个面向六年级学生和年长家长的中文学习网页，重点是：打开链接即可使用、大字清楚、无需注册、孩子先练习再查看分步讲解。

当前建议形态是网页/PWA，而不是原生 Mac 应用。网页可以直接转发链接，也可以在 Mac 上添加到程序坞。

## 当前已完成

- `app/page.tsx`
  - 家长友好的首页和使用说明。
  - 数学练习题库：分数、比和比例、圆与百分数，共 18 道内置题。
  - 可以组合选择题库，并选择每轮练习 5、10 或 15 题。
  - 选择答案后显示正确/错误反馈、提示、逐步讲解和下一题按钮。
  - “教材中心”目前只保留语文、数学、英语三个入口。
  - 教材入口指向国家中小学智慧教育平台和 ChinaTextbook 对应目录，不把整套教材 PDF 重新公开托管。
- `app/globals.css`
  - 家长友好的暖色视觉、较大字号、响应式布局。
  - 适配 Mac 桌面和窄屏设备。
- `app/layout.tsx`
  - 中文页面元信息、网页标题和 PWA manifest。
- `public/manifest.webmanifest`
  - 支持在 Mac 浏览器中以类似应用的方式添加到程序坞。
- `tests/rendered-html.test.mjs`
  - 验证页面能服务端渲染，并检查练习区、分步讲解提示和三科教材中心。

## 本地运行

```bash
npm install
npm run dev
```

浏览器打开 `http://localhost:3000/`。

验证命令：

```bash
npm test
npm run build
```

当前 `npm test` 已通过。

## 重要边界

1. 当前版本是内置题库和确定性分步讲解，不是可以识别任意拍照题目的大模型讲题服务。
2. GitHub Pages 适合发布当前这种静态网页，但页面通常是公开的。不要把 API 密钥、儿童隐私信息或未获授权的教材 PDF 放进公开仓库。
3. 完整教材 PDF 只有在用户合法获取并确认允许分享时，才可以考虑上传；默认使用正规教材入口链接。
4. 若要支持“上传教材后自动生成练习”和“任意题目 AI 讲解”，需要后端服务或受保护的 API，不能把密钥写进 GitHub Pages 前端。

## Git / Sites 状态

- 当前本地分支：`main`
- 最近项目提交：`6c2d1e5`（刷新交接状态）；README 为 `a5f677f`，核心功能版本为 `feee052`。
- `.openai/hosting.json` 已保存 Sites 项目配置。
- Sites 已保存一个可部署版本，但因为当前环境不支持外部邮箱访客邀请，所以没有部署成父母可访问的私有链接。
- GitHub 已创建公开仓库：`https://github.com/xc962983-ctrl/yibu-yibu-grade6-practice`。仓库内有 README、此交接文件和完整源文件压缩包；本地 `origin` 仍是临时 Sites 源码仓库，不要把 `byoungd/up` 当作目标仓库。

## 下一位 Codex 的建议工作顺序

1. 从 GitHub 仓库下载 `yibu-yibu-grade6-practice-source-v2.tar.gz`，解压到工作目录。
2. 检查 `git status -sb` 和 `npm test`，确认交接包可运行。
3. 如需持续开发，先把本地 `origin` 改成 GitHub 仓库地址，再按用户要求提交代码。
4. 使用 GitHub Actions 构建并发布 GitHub Pages；项目不是 Jekyll 内容，需要发布构建后的静态产物。
5. 将 GitHub Pages 地址交给用户，让父母直接打开；如需像应用一样使用，指导他们把网页添加到 Mac 程序坞。
6. 如果用户确认拥有教材文件且允许分享，再设计受控的教材存储方式；不要默认把整套教材 PDF 放进公开 GitHub 仓库。
7. 如果要加入真正的 AI 自动讲题，先确认模型供应商、预算、隐私要求和后端部署方式，再扩展功能。

## 不要做的事

- 不要把项目推到原始的 `https://github.com/byoungd/up`。
- 不要把任何 API key 写进前端代码或 GitHub 仓库。
- 不要未经确认批量下载并重新公开完整教材 PDF。
- 不要把“内置示例题讲解”描述成“支持任意题目自动讲解”。
