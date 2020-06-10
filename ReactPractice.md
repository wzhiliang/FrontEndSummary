### React 实操

###### -  1. 创建工程文件夹，用vscode打开文件夹。

> mkdir react-demo

> cd react-demo

> code .

###### -  2. npm init初始化package.json

###### -  3. 安装依赖包

> npm install react react-dom webpack webpack-cli webpack-dev-server html-webpack-plugin -D

> npm install babel-core babel-loader babel-plugin-transform-runtime -D

> npm install babel-preset-env babel-preset-stage-0 babel-reset-react -D

> npm install babel-preset-react -D

> npm install babel-loader@7 -D

###### - 4. 在根目录下创建src文件夹，在src中创建index.html  index.js

###### - 5. 创建webpack.config.js

``` 
const path = require('path');
const HtmlWebpackPlugin = require('html-webpack-plugin');

// 负责将html文档虚拟到根目录下
let htmlWebpackPlugin = new HtmlWebpackPlugin({
    // 虚拟的html文件名 index.html
    filename: 'index.html',
    // 虚拟html的模板为 src下的index.html
    template: path.resolve(__dirname, './src/index.html')
})

module.exports = {
    // 开发模式
    mode: 'development',
    // 配置入口文件
    entry: './src/index.js',
    // 出口文件目录为根目录下dist, 输出的文件名为main
    output: {
        path: path.resolve(__dirname, 'dist'),
        filename: 'main.js'
    },
    // 配置开发服务器, 并配置自动刷新
    devServer: {
        // 根目录下dist为基本目录
        contentBase: path.join(__dirname, 'dist'),
        // 自动压缩代码
        compress: true,
        // 服务端口为1208
        port: 1208,
        // 自动打开浏览器
        open: true
    },
    // 装载虚拟目录插件
    plugins: [htmlWebpackPlugin],
}
```

###### - 6.创建.babelrc
``` json
{
    "presets": ["env", "stage-0", "react"],
    "plugins": ["transform-runtime"]
}
```

###### - 7.在webpack.config.js中加入loader
``` javascript
// webpack.config.js
module.exports = {
    ...
    // 配置loader
    module: {
        // 根据文件后缀匹配规则
        rules: [
            // 配置js/jsx语法解析
            { test: /\.js|jsx$/, use: 'babel-loader', exclude: /node_modules/ }
        ]
    }
};
```

**安装的loader这些都是老版本的**




