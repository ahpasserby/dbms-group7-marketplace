# 前后端接口约定

接口放在 `public/api/<模块>/`。从 `public/` 下的页面用相对路径调用，例如 `./api/items/list.php`。

## 请求与响应

- 查询用 `GET`，参数放在 URL。写操作用 `POST`，请求体用 `application/json`。上传图片用 `multipart/form-data`。
- PHP 从 Session 读取用户身份，检查操作权限。写请求通过 `X-CSRF-Token` 传递令牌，由后端校验。
- 接口返回 JSON。成功结果放在 `data`，失败返回 `error.code` 和 `error.message`。前端按错误码处理，向用户显示提示文字。
- 列表从 `page=1` 开始，`page_size` 默认 20，最多 50。PHP 用 `meta.query_ms` 返回数据库查询耗时（毫秒），前端负责显示。

## 字段

| 类型 | 约定 | 示例 |
| --- | --- | --- |
| 名称 | 数据库、JSON、表单统一用 `snake_case` | `item_id`、`seller_id` |
| 金额 | 单位为元，数据库用 `DECIMAL(10,2)`，JSON 用字符串 | `"39.90"` |
| 时间 | 字段以 `_at` 结尾，接口返回 UTC，页面按北京时间显示 | `"2026-11-20T08:00:00Z"` |
| 空值 | 尚未填写或发生的值用 `null` | `"completed_at": null` |

## 预约商品（接口草案）

| 项目 | 内容 |
| --- | --- |
| 请求 | `POST ./api/orders/reserve.php`，请求体 `{"item_id":128}` |
| 权限 | 用户已登录，且商品属于其他卖家 |
| 成功 | HTTP 201 · `{"data":{"order_id":506,"order_status":"reserved"}}` |
| 商品已被预约 | HTTP 409 · `{"error":{"code":"item_unavailable","message":"商品已被预约"}}` |
| 其他错误 | 400 参数有误，401 未登录，403 无权限，404 商品不存在 |

预约时，后端在同一事务中将商品从 `available` 改为 `reserved` 并创建订单。两个买家同时预约同一件商品，只能有一个成功。

## 协作

新增接口先在本文写明方法、路径、权限、入参、响应和数据变化。改表时，SQL 和接口代码放在同一个 PR，注明执行顺序。合并到 `main` 会发布 `public/` 下的网站文件，数据库变更需单独执行。
