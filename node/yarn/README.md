在yarn发布之前，所有Nodejs开发者用的都是npm包管理工具，而npm工具存在挺多难以忍受的诟病，包括安装速度慢、每次都要在线重新安装等问题，而yarn也是为了解决npm当前所存在的问题而出现的。

### 安装
2. 如果原先有npm工具的话，安装yarn很简单，只需要一行命令即可

```
npm install -g yarn

```
2. 如果没有npm工具，安装yarn可参照   
[各平台下yarn工具安装方式](https://yarnpkg.com/en/docs/install)
### 配置
安装yarn之后默认的包安装源是https://registry.yarnpkg.com，可用查看命令

```
yarn config get registry

```
若想提高yarn安装的速度，可将包安装源修改为cnpm的安装源，执行以下命令即可
```
yarn config set registry 'https://registry.npm.taobao.org'
```
### 使用
初始化某个项目
```
npm init  
yarn init  
```
默认的安装依赖操作
```
npm install/link
yarn install/link
```
安装某个依赖，并且默认保存到package
```
npm install xxx —save
yarn add xxx
```
移除某个依赖项目
```
npm uninstall xxx —save
yarn remove xxx
```
安装某个开发时依赖项目
```
npm install --save-dev xxx
yarn add xxx —dev
```
更新某个依赖项目
```
npm update --save xxx
yarn upgrade xxx
```
安装某个全局依赖项目
```
npm install -g xxx
yarn global add xxx
```
发布/登录/登出，一系列NPM Registry操作
```
npm publish/login/logout
yarn publish/login/logout
```
运行某个命令
```
npm run/test
yarn run/test
```
