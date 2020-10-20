## 1、下载并配置less
使用create-react-app脚手架创建的项目，默认不支持less。
### 直接修改webpack的配置
- 运行npm run eject
- 在webpack.config.js中进行修改
在oneOf中添加 

```javascript
{
    test:/\.less$/,
  use:['style-loader','css-loader','less-loader']
}
```
### 或者使用中间件
- craco库，@craco/less插件
- customize-cra react-app-rewired库
## 2、使用Mock
- 数据模板定义规范：
数据模板中的每个属性由 3 部分构成：属性名(name)、生成规则(rule)、属性值(value)
语法：'name|rule': value
生成规则 有 7 种格式：

```javascript
'name|min-max': value
'name|count': value
'name|min-max.dmin-dmax': value
'name|min-max.dcount': value
'name|count.dmin-dmax': value
'name|count.dcount': value
'name|+step': value
```
## 3、Antd的按需加载
### 使用 craco 库
1. 安装库：npm i @craco/craco
2. 安装插件：npm i craco-antd
3. 创建配置文件 ，在项目根目录下创建 craco.config.js
4. 编写配置
```javascript
const CracoAntDesignPlugin = require("craco-antd");
   module.exports = {
       plugins: [{ plugin: CracoAntDesignPlugin }]
   };
   ```
5. 修改启动命令           
 start:"react-scripts start"修改成： start:"craco start"
 
### 使用customize-cra库
1. 安装库：npm i customize-cra react-app-rewired 
2. 安装插件：npm i bable-plugin-import
3. 创建配置文件，在项目根目录下创建 config-overrides.js
4. 编写配置   
```javascript
const { override,fixBabelImports } = require('customize-cra');
 module.exports = override(fixBabelImports('import', {
  "libraryName": "antd",
  "libraryDirectory": "es",
  "style": "css"
 }))
 ```
5. 修改启动命令
```javascript
   start:"react-scripts start"  修改成：start:"react-app-rewired start"
   ```
### 使用eject命令
1. npm run eject运行这个命令后，会把配置文件暴露出来，可以直接修改项目的配置文件
2. 安装babel插件  babel-plugin-import
3. 在根目录下创建.babelrc配置文件
4. 注意：如果使用这种方式，需要把package.json文件中的babel字段删除
5. 在配置文件中添加插件功能
```javascript
{
     "presets":["react-app"],//解析react的意思
     "plugins": [
         ["import", {
         "libraryName": "antd",
        "libraryDirectory": "es",
         "style": "css" // `style: true` 会加载 less 文件
         }]
 ]
 }
 ```
