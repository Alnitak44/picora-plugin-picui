# PICUI 图床

为 Picora 添加 [PICUI](https://picui.cn/) 图片上传支持。接口和响应字段依据 [PICUI 官方接口文档](https://picui.cn/page/api-docs.html)。

## 使用

1. 在 Picora 1.0.1 或更新版本中安装本插件 ZIP，新增「PICUI 图床」配置。
2. 游客上传：将「授权信息」留空。
3. 账户上传：在 PICUI 个人中心取得 Token，并在「授权信息」中填写 `Bearer `（含末尾空格）加 Token，例如 `Bearer 1|你的Token`。
4. 选择图片上传。插件读取返回的图片直链和缩略图链接。

**注意：**「授权信息」填写的是完整的 HTTP Authorization 请求头值，不要只填 Token。留空时，Picora 不发送 Authorization 请求头，PICUI 会按游客上传处理。

## 请求与限制

插件只向 `https://picui.cn/api/v1/upload` 发送 POST 请求，以 multipart/form-data 的 `file` 字段发送单张图片，设置 `Accept: application/json`。仅在 HTTP 成功且响应 `status` 为 `true` 时视为上传成功，直链取自 `data.links.url`。请求不会跟随重定向，也不会自动重传。

PICUI 的可用额度、游客上传规则与图片保存期限由 PICUI 决定。此插件只负责上传；管理或删除图片请前往 PICUI 网站。

## 许可

[MIT](LICENSE)。这是第三方适配插件，不代表 PICUI 官方。
