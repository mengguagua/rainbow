# rainbow

> gcc's project

#### Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:9080
npm run dev

# build electron application for production
npm run build

# run unit & end-to-end tests
npm test


# lint all JS/Vue component files in `src/`
npm run lint

```

---

This project was generated with [electron-vue](https://github.com/SimulatedGREG/electron-vue) using [vue-cli](https://github.com/vuejs/vue-cli). Documentation about the original structure can be found [here](https://simulatedgreg.gitbooks.io/electron-vue/content/index.html).

#### 可能遇到的报错处理

在 .electron-vue/webpack.renderer.config.js 和 .electron-vue/webpack.web.config.js 文件中找到 `HtmlWebpackPlugin` 代码段并更改为如下代码：

```
 new HtmlWebpackPlugin({
  filename: 'index.html',
  template: path.resolve(__dirname, '../src/index.ejs'),
  templateParameters(compilation, assets, options) {
    return {
      compilation: compilation,
      webpack: compilation.getStats().toJson(),
      webpackConfig: compilation.options,
      htmlWebpackPlugin: {
        files: assets,
        options: options
      },
      process,
    };
  },
  minify: {
    collapseWhitespace: true,
    removeAttributeQuotes: true,
    removeComments: true
  },
  nodeModules: process.env.NODE_ENV !== 'production'
    ? path.resolve(__dirname, '../node_modules')
    : false
}),
```

