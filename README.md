# marknote

一个简单的 github pages 主页。

特性：

- 支持 markdown 书写文章、目录
- 极简主义，回归本心
  - 纯手工编辑目录（markdown 语法）
  - 纯前端项目，**因此也不支持 SEO，也不计划支持**
  - 自带简洁样式
- 支持大屏、小屏设备
- 自带打印机优化样式，通过浏览器打印功能，方便导出为 pdf 文件

## 使用

首先是 `git clone` 这个项目，然后打开你喜欢编辑器，可以开始写作了。

## 约定

- 整个页面基本是手工编辑的。固定的文件主要有 `SIDEBAR.md` 和 `README.md`
  - `README.md` 是主页，如同 github 的仓库
  - `SIDEBAR.md` 是侧栏的内容。一般用作目录使用
- 文章应该统一放置到 `docs` 目录下
  - docs 目录里的内容可以自由组织

## 自定义配置

所有自定义的配置内容都在 `index.html` 里的 `window.marknoteConfig` 代码。

```js
window.marknoteConfig = {
  siteName: '站点名称' // 网站的名称，最终会显示为窗口的标题及顶部导航的左则
}
```

## 侧栏

现在已经支持多个侧栏文件，默认使用 `SIDEBAR.md`，通过的连接中指定 `sidebar=xxxx.md` 可以指定使用侧栏文件。

如： 

在 `index.html` 中

```html
<!-- ... -->
<a href="/#/docs/deploy-on-github.md?sidebar=guide-sidebar.md">部署</a>
<!-- ... -->
```

在 `SIDEBAR.md` 中也支持指定侧栏：

```md
- [部署到 github pages](docs/guide/deploy-on-github.md)
- [部署到 codeberg pages](docs/guide/deploy-on-codeberg.md)
```


## 修改样式、二次开发

核心代码在 [src/index.js](src/index.js)，需要使用 nodejs 进行构建。全部样式目前都在 [src/style.css](src/style.css)。

## LICENSE

[MIT](LICENSE)
