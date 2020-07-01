# npm 和 yarn 的区别

npm 和 yarn 都是包管理工具，都可以安装包和模块，大家都应该用过这两个包管理工具，用 npm 后会生成一个 package-lock.json 的文件，用 yarn 过后会生成一个 yarn.lock 的文件，接下来说一下这两个包管理工具：

以目前的情况来看，大家都支持使用 yarn 而不是 npm，原因是：

#### 1、yarn 的速度快。

-   并行安装：npm 和 yarn 在执行包的安装时，都会执行一系列任务。npm 是按照队列执行每个 package，必须要等到当前 package 安装完成之后，才能继续后面的安装。而 yarn 是同步执行所有任务，提高了性能。

-   离线模式：如果之前已经安装过一个软件包，用 yarn 再次安装时之间从缓存中获取，就不用像 npm 那样再从网络下载了。

-   安装版本统一:为了防止拉取到不同的版本，yarn 有一个锁定文件 记录了被确切安装上的模块的版本号。每次只要新增了一个模块，yarn 就会创建（或更新）yarn.lock 这个文件,每一次拉取同一个项目依赖时，使用的都是一样的模块版本;npm 其实也有办法实现处处使用相同版本的 packages，但需要开发者执行 npm shrinkwrap 命令,通过 shrinkwrap 命令生成 npm-shrinkwrap.json 文件，只有当这个文件存在的时候，packages 版本信息才会被记录和更新。

#### 2、更简洁的输出。

-   npm 的输出信息比较冗长。在执行 npm install 的时候，命令行里会不断地打印出所有被安装上的依赖。相比之下，yarn 简洁太多：默认情况下，结合了 emoji 直观且直接地打印出必要的信息，也提供了一些命令供开发者查询额外的安装信息。

#### 3、多注册来源处理。

-   所有的依赖包，不管他被不同的库间接关联引用多少次，安装这个包时，只会从一个注册来源去装，要么是 npm 要么是 bower, 防止出现混乱不一致。

#### 4、更好的语义化。

yarn 改变了一些 npm 命令的名称，比如 yarn add/remove，感觉上比 npm 原本的 install/uninstall 要更清晰。

#### 5、yarn 和 npm 命令对比

-   查看版本

```
yarn --version
npm -version(或者 node -v)
```

-   安装淘宝镜像

```
yarn config set registry 'https://registry.npm.taobao.org'
npm install -g cnpm --registry=http://registry.npm.taobao.org
```

-   初始化项目

```
yarn init
npm init
```

-   默认安装项目依赖

```
yarn install
npm install
```

-   安装某个依赖，并且默认保存到 package

```
yarn add xxx
npm install xxx --save
```

-   卸载项目某个依赖

```
yarn remove xxx
npm uninstall xxx --save
```

-   更新某个项目依赖

```
yarn upgrade xxx
npm update xxx --save
```

-   安装某个全局的项目依赖

```
yarn global add xxx
npm install xxx -g
```

-   安装某个特定版本号的项目依赖

```
yarn add xxx@
npm install xxx@1.2.33 --save
```

-   发布/登录/登出，一系列 NPM Registry 操作

```
yarn publish/login/logout
npm publish/login/logout
```

-   运行某个命令

```
yarn run/test
npm run/test
```
