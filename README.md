# ACF MUI Page Builder

WordPress 插件，为 Advanced Custom Fields (ACF) 提供「Page Builder」字段类型，配合外部 MUI 编辑器进行可视化页面搭建。

## 要求

- **WordPress** 6.2+
- **PHP** 8.2+
- [Advanced Custom Fields](https://www.advancedcustomfields.com/) (ACF)
- [JWT Authentication for WP REST API](https://wordpress.org/plugins/jwt-auth/)（用于编辑器与 WordPress REST API 的鉴权）

可选：

- [FileBird](https://wordpress.org/plugins/filebird/) — 若已安装，媒体库接口将使用 FileBird；否则使用内置媒体库接口
- [WPML](https://wpml.org/) — 若已安装，可为每种语言单独配置编辑器 URL

## 安装

1. 确保已安装并启用 ACF 与 JWT Auth 插件。
2. 将本插件放入 `wp-content/plugins/acf-mui-page-builder`，或在后台通过「安装插件」上传。
3. 在 WordPress 后台启用 **ACF MUI Page builder**。

## 配置

1. 在后台进入 **设置 → MUI Page builder**。
2. 设置 **Editor URL**：指向你的 MUI 页面编辑器前端地址（若使用 WPML，可为每种语言设置不同 URL）。
3. 在 ACF 中创建字段组，添加字段类型 **Page builder**，并绑定到需要的文章类型（如「页面」）。

## 功能概览

- **Page Builder 字段**：在编辑页中嵌入 iframe，加载外部 MUI 编辑器；保存时通过 ACF 将 blocks 数据写入 `blocks` 字段。
- **REST API**：为编辑器提供配置、媒体库（或 FileBird）、自动完成等接口，使用 JWT 鉴权。
- **Revisions**：每次保存页面时对 `blocks` 做一次快照，在页面编辑页的「Page Builder Revisions」 metabox 中可查看/删除历史；最多保留 20 条（可在 `MuiPageBuilderRevisions::MAX_REVISIONS` 中修改）。WordPress 自带页面修订已对本插件关闭（`wp_page_revisions_to_keep` 设为 0）。
- **单栏编辑页**：页面编辑屏幕强制单栏布局，便于大屏编辑器使用。

## 开发

```bash
composer install   # 若有依赖
```

前端编辑器入口为 `AcfFieldMuiPageBuilder` 引用的 `dist/main.js`，需在仓库外或本仓库内单独构建后放入 `dist/`。

## 许可证

GPL-3.0-or-later
