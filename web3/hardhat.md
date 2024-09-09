


> Written with [StackEdit中文版](https://stackedit.cn/).

**Node.js**是一个基于JavaScript的运行时环境，用于在服务器端执行JavaScript代码。于2009年创建，构建在Google Chrome的V8 JavaScript引擎之上。Node.js的主要目的是让开发者能够使用JavaScript在服务器端编写高性能的、可扩展的网络应用程序。

**npm**（Node Package Manager）是Node.js的包管理工具和包管理器，于2010年创建。npm是Node.js生态系统的重要组成部分，为Node.js开发者提供了一个强大的工具来管理和共享JavaScript代码包（packages）和模块（modules）。

npm国内镜像源设置
```javascript
npm config set registry=http://registry.npm. taobao. org
```

在工程目录内的命令行输入`npm init`初始化工程
安装hardhat：`npm i --save-dev hardhat`
使用hardhat创建工程模板：`npx hardhat init`
编译合约：`npx hardhat compile`
开启节点：新打开一个终端`npx hardhat node`
部署合约在节点中：`npx hardhat run .\folder\file (--network localhost)`运行在线程里( 节点 )中
运行单元测试`npx hardhat test (.\test\file) (--network localhost)`( 在节点上 )运行所有( 指定 )文件的单元测试
测试和部署的时候都会自动编译

开启hardhat控制台与合约交互（不常用）`npx hardhat console (--network localhost)`

## 配置变量
可以将配置变量用于特定于用户的值或不应包含在代码存储库中的数据。这些变量是通过`vars`范围内的任务设置的，并且可以使用`vars`对象在配置中检索。

- 配置变量以纯文本形式存储在磁盘上。避免将此功能用于通常不会保存在未加密文件中的数据。运行`npx hardhat vars path`以查找存储的文件位置。

`npx hardhat vars set` 为配置变量分配一个值，如果不存在则创建一个
`npx hardhat vars get`显示配置变量的值
`npx hardhat vars list`打印存储在计算机上的所有配置变量
`npx hardhat vars delete`删除配置变量

### 在配置文件中使用变量
可以在 Hardhat 配置文件中检索您之前存储的配置变量。使用`vars.get`方法获取它们：
```javascript
const INFURA_API_KEY = vars.get("INFURA_API_KEY");
```
对于可能不存在的变量，可以指定默认值作为第二个参数：
```javascript
const salt = vars.get("DEPLOY_SALT", "12345");
```
还可以使用`vars.has`检查变量是否存在：
```javascript
const accounts = vars.has("TEST_PK") ? [vars.get("TEST_PK")] : [];
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbNjk0MDMyOTg1LC0zMDY2MTc5MTksLTMwNj
YxNzkxOSw2NTA2MDM1OTcsLTM2NzUyMjAwLDEwODk5NDQ0NDYs
LTk2NjcxMDYzOSwtMTU5MTE3NjQzOCwtMTc4MzY1NjE0NiwxMD
Q4NTcxNTA3XX0=
-->