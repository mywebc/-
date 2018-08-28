# webpack notes
## 入口函数（entry）
> 字符串
* 单个文件，唯一入口(入口模块)
> 字符串数组
* 所有模块立即加载，最后一个会被导出
> 对象
* 创建多个入口，会打多次包，键就是包的名字（可以是字符串或者是数组）
## loaders
## plugins
## externals(不被打包)
## ProvidePlugin（第三方库写在这里，比如jquery）