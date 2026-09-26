# qx-market-catalog

QxSSH 插件市场：应用目录与版本包（无服务器形态，纯静态托管）。

## 目录结构

- `catalog/catalog.json` — 应用目录（唯一入口，含各版本 sha256 与 size）
- `catalog/CHECKSUMS.txt` — 每行 `<sha256>  <zip相对路径>`（两空格，兼容 `sha256sum -c`）
- `catalog/apps/<id>/<version>.zip` — 各版本应用包
- `plugins/` — 市场插件自身安装包（`qx-market-<version>.zip`，后续上架）

## 消费方式

- jsDelivr（浏览器可用，带 `Access-Control-Allow-Origin: *`）：
  `https://cdn.jsdelivr.net/gh/koharachan/qx-market-catalog@main/catalog/catalog.json`
- raw（服务端/CLI 可达，无 ACAO，浏览器跨域 fetch 会被 CORS 拦截）：
  `https://raw.githubusercontent.com/koharachan/qx-market-catalog/main/catalog/catalog.json`

zip 下载地址 = catalog 基准 URL + catalog.json 中的 `zip` 相对路径（如 `apps/hello-app/1.0.0.zip`）。
下载后必须用 `sha256` 字段校验（Web Crypto `crypto.subtle.digest('SHA-256')`），不符拒绝安装。
