npm安装包
```
npm install packagename
//安装名为packagename的依赖包

npm install packagename -g
//将包安装到全局环境中

npm install packagename --save
//安装的同时,将信息写入package.json的dependencies中,代表应用运行时依赖的包

npm install packagename --save-dev
//安装的同时,将信息写入package.json的devDependencies中,代表应用开发时依赖的包
```

npm其他命令
```
npm init
//会引导你创建一个package.json文件，包括名称、版本、作者这些信息等

npm remove packagename
//移除已安装的包packagename

npm update packagename
//更新已安装的包packagename

npm ls
//列出当前安装了的包,树状结构代表了安装的依赖关系

npm root
//查看当前工程包的安装路径

npm root -g
//查看包的全局安装路径

npm help
//帮助，如果要单独查看install命令的帮助，可以使用的npm help install
```
