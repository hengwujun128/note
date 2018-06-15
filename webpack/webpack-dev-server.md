## 1.basic

[tutorial](https://github.com/webpack/docs/wiki/webpack-dev-server)

> 1.content-base

The webpack-dev-server will serve the files in the current directory, unless you configure a specific content base.

```
"dev": "webpack-dev-server --content-base ./dev --env=webpack.dev --open --hot",
```

- **webpack-dev-server 为当前目录 dev 下的静态资源提供服务**

> 2.demo

```
var path = require("path");
module.exports = {
  entry: {
    app: ["./app/main.js"]
  },
  output: {
    path: path.resolve(__dirname, "build"),
    publicPath: "/assets/",
    filename: "bundle.js"
  }
};

webpack-dev-server --content-base build/
```

You have an app folder with your initial entry point that webpack will bundle into a bundle.js file in the build folder.

- app 目录下的入口文件 main.js 会打包到 build 目录下 bundle.js
- **webpack-dev-server 为当前目录 build 下的静态资源提供服务，同时 build 也为打包的输出目录**
- 被更改的包（bundle.js）来自于内存，它相对于 publicPath;它不会输入到 outPut 目录，当一个 bundle 已经存在于同一个 URL，内存的 bundle 具有优先权

This modified bundle is served from memory at the relative path specified in publicPath (see API). It will not be written to your configured output directory. Where a bundle already exists at the same URL path, the bundle in memory takes precedence (by default).

Using the configuration above, the bundle is available at localhost:8080/assets/bundle.js.

> 3.  To load your bundled files, you will need to create an index.html file in the **build folder from which static files are served(--content-base option)**

```
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <title>Document</title>
</head>
<body>
  <script src="assets/bundle.js"></script>
</body>
</html>
```

By default, go to localhost:8080/ to launch your app. In this example's configuration (with publicPath), go to localhost:8080/assets/

> 4.demo2

```
module.exports = {
  entry: './dev/index.js',
  output: {
    path: path.resolve(__dirname, './dev'),
    publicPath: '/dev/', // webpack-dev-server 根目录
    filename: 'build.js'
  },
  module: {
    rules: [{
        test: /\.vue$/,
        loader: 'vue-loader',
      },
      {
        test: /\.js$/,
        loader: 'babel-loader',
        exclude: /node_modules/
      },
    ]
  },
  devServer: {
    noInfo: true
  },
  performance: {
    hints: false
  },
  devtool: '#eval-source-map'
}
```
