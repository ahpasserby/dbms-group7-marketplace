# COMP3013 · Group 7 二手交易平台

小组开发期间使用 InfinityFree 联调，课程验收使用 XAMPP。[联调网站](https://dbmsgroup7.freedev.app/)

## 加入开发

把你的 **GitHub 用户名**发给项目负责人。接受仓库邀请后，首次开发先克隆代码：

```sh
git clone https://github.com/ahpasserby/dbms-group7-marketplace.git
cd dbms-group7-marketplace
```

以后每次开工，在仓库里运行 `git switch main` 和 `git pull --ff-only`，再修改 `public/` 下的 HTML、CSS 和 JavaScript。首页是 `public/index.html`，PHP 接口放在 `public/api/`。页面需要读写数据时，先看[前后端接口约定](docs/api.md)。

## 提交改动

**当前允许直接推送到 `main`。** 提交信息遵循 Conventional Commits，例如 `feat: 添加商品详情页`、`fix: 修复价格显示`。下面以修改首页为例，`git add` 后面换成本次改动的文件：

```sh
git status --short
git add public/index.html public/home.css
git commit -m "feat: 添加首页商品入口"
git pull --rebase origin main
git push origin main
```

如果 push 时提示远端已有新提交，再执行一次 `git pull --rebase origin main`。遇到冲突时和修改同一文件的组员确认内容，解决后再推送。

## 部署与数据库

`main` 上的 `public/` 有改动时，GitHub Actions 会通过 FTPS 把网站文件同步到 InfinityFree 的 `htdocs/`。推送后在 [Actions](https://github.com/ahpasserby/dbms-group7-marketplace/actions/workflows/deploy.yml) 查看结果，显示绿色 ✓ 后刷新联调网站即可。

数据库表结构和数据由项目负责人单独导入。页面需要新增或修改字段时，把字段名、用途和对应页面发给负责人。
