# 概念
* 入口（entry）webpack构建的入口/可以多个
* 输出（output）webpack输出路径/可以多个
* loader 文件类型转换器，test/use
* plugins 全局任务处理
* mode 设置不同的环境，处理时用不同的webpack优化
## entry
> 字符串或者字符串数组
* 单个文件入口，缺乏灵活性，如果是字符串数组，所有模块都会加载，最后一个模块导出。
> 对象
* 可扩展性强，可以打包多个文件，常用场景用已分应用程序和第三方库，例:
```javascript
    entry: {
        app: './src/app.js',
        vendors: './src/vendors.js'
    }
```
* 也可以用于打包多页面应用程序
## output
> 必须指定两个属性filename和path(绝对路径) 例：
```javascript
    output: {
        filename: 'bundle.js',
        path: '/home/proj/public/assets'
    }
```
> 当有多个入口文件时，输出确保每个文件有唯一Id,使用占位符
```javascript
    entry: {
        app: './src/app.js',
        search: './src/search.js'
    },
    output: {
        filename: '[name].js',
        path: __dirname + '/dist'
    }
```
* [name]表示使用入口文件的名字，还可以使用[id]/webpack构建时随机生成的id，[hash]生成的hash值等。
> publicPath用于设置静态资源CDN
```javascript
  output: {
    path: "/home/proj/cdn/assets/[hash]",
    publicPath: "http://cdn.example.com/assets/[hash]/"
}
```
* 项目入口也要加上
```javascript
    entry: {
        __webpack_public_path__ = myRuntimePublicPath
    }
```
## mode(模式)
* mode: string "development" "production" 
```javascript
    module.exports = {
        mode: 'development',
    };  
```
* 或者通过命令行的形式
```javascript
"scripts": {  
      "dev": "webpack --mode development",  
      "build": "webpack --mode production"  
  }, 
```
## loader（三种方法）
> 写在module中,除了test/use,还可以指定options（推荐）
```javascript
  module: {
    rules: [
      {
        test: /\.css$/,
        use: [
          { loader: 'style-loader' },
          {
            loader: 'css-loader',
            options: {
              modules: true
            }
          }
        ]
      }
    ]
  }
```
> require语句导入，！分割,?可以传参
```javascript
import Styles from 'style-loader!css-loader?modules!./styles.css';
```
> 命令行,--module-bind绑定
```javascript
webpack --module-bind jade-loader --module-bind 'css=style-loader!css-loader'
```
## plugins
> 一般向plugins属性传入 new 实例。
```javascript
 plugins: [
    new webpack.optimize.UglifyJsPlugin(),
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
```