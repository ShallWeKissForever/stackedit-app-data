


> Written with [StackEdit中文版](https://stackedit.cn/).

**Node.js**是一个基于JavaScript的运行时环境，用于在服务器端执行JavaScript代码。它是由Ryan Dahl于2009年创建的，并且构建在Google Chrome的V8 JavaScript引擎之上。Node.js的主要目的是让开发者能够使用JavaScript在服务器端编写高性能的、可扩展的网络应用程序。

**npm**（Node Package Manager）是Node.js的包管理工具和包管理器，最初由Isaac Z. Schlueter于2010年创建。npm是Node.js生态系统的重要组成部分，为Node.js开发者提供了一个强大的工具来管理和共享JavaScript代码包（packages）和模块（modules）。

npm国内镜像源设置
```
npm config set registry=http://registry.npm. taobao. org
```

在工程目录内的命令行输入`npm init`初始化工程
安装hardhat：`npm i --save-dev hardhat`
使用hardhat创建工程模板：`npx hardhat`，后续使用这个命令是帮助
编译合约：`npx hardhat compile`
开启节点：新打开一个终端`npx hardhat node`
部署合约在节点中：`npx hardhat run .\folder\file (--network localhost)`运行在线程里( 节点 )中
运行单元测试`npx hardhat test (.\test\file) (--network localhost)`( 在节点上 )运行所有( 指定 )文件的单元测试
测试和部署的时候都会自动编译

开启hardhat控制台与合约交互（不常用）`npx hardhat console (--network localhost)`

配置变量
可以将配置变量用于特定于用户的值或不应包含在代码存储库中的数据。

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTA4OTk0NDQ0NiwtOTY2NzEwNjM5LC0xNT
kxMTc2NDM4LC0xNzgzNjU2MTQ2LDEwNDg1NzE1MDddfQ==
-->