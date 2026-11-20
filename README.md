# COMP3013 · Group 7 二手交易平台

小组开发期间使用 InfinityFree 联调，project 提交使用 XAMPP。[开发网站](https://dbmsgroup7.freedev.app/)

## 加入开发

把你的 **GitHub 用户名**发给 [Sarzn](v530026271@mail.bnbu.edu.cn)

- 接受仓库邀请后，先克隆仓库
- 以后每次开工，在仓库修改 `public/` 下的 HTML、CSS 和 JavaScript

首页是 `public/index.html`
PHP 接口放在 `public/api/`
文档是 `docs/api.md`, 页面需要读写数据时请首先查看文档, 需要新增接口时候请首先修改文档!!

## 提交改动

**当前允许直接推送到 `main`。** 提交信息遵循 Conventional Commits，例如 `feat: 添加商品详情页`、`fix: 修复价格显示`

建议先 rebase, 遇到冲突时注意甄别, 可能的话和其他人商讨

## 部署与数据库

`main` 上的 `public/` 有改动时，GitHub Actions 会通过 FTPS 把网站文件同步到 InfinityFree 的 `htdocs/`

> 推送后在 [Actions](https://github.com/ahpasserby/dbms-group7-marketplace/actions/workflows/deploy.yml) 查看结果，显示绿色 ✓ 后刷新联调网站即可。

数据库表结构和数据由[Sarzn](v530026271@mail.bnbu.edu.cn) 单独导入

- 页面需要新增或修改字段时，把字段名、用途和对应页面**更新到文档!**并且规范提交, 最好是顺便给 [Sarzn](v530026271@mail.bnbu.edu.cn) 微信发条 1
