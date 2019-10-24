## NPM

### 1. 查看安装的模块

```shell
npm list
npm list --depth=0
npm list --depth=0 --global
npm list <packagename>
// 查看npm服务器上所有的jquery版本信息
npm view jquery 
// 查看jquery的所有的版本
npm view jquery versions
// 查看本地安装的jQuery
npm ls jquery
// 查看全局安装的jquery
npm ls jquery -g
// 安装指定版本
npm install --save-dev react-router@2.8.1
// 全局包位置
npm root -g
// npm 安装位置
which npm
// node 安装目录
which node
```

### 2. npm权限

npm install 报权限错误（node-sass，node-gyp 等）涉及到底层编译

```shell
npm install  --unsafe-perm
npm config set unsafe-perm	针对当前用户的） 
npm config -g set unsafe-perm 	(全局的）
```

### 3. 版本管理

```shell
// 查看node所有版本
npm view node versions
//清除nodejs的cache：
npm cache clean -f 
//使用npm安装n模块
npm install -g n 
sudo n latest // 升级到最新版本
sudo n stable // 升级到稳定版本
sudo n xx.xx // 升级到具体版本号
```

