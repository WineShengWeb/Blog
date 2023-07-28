<!--
 * @Author: gxg<18215084858@163.com>
 * @Date: 2023-02-28 15:27:34
 * @LastEditors: gxg<18215084858@163.com>
 * @LastEditTime: 2023-02-28 15:29:51
 * @Description: gitignore文件配置
-->

### gitignore 文件配置

```
# 以'#'开始的行，被视为注释

# macOS 操作系统上的一个不可见文件

.DS_Store

# _ 忽略所有文件(_)

-

# 忽略 node_modules 下所有文件

node_modules

# 忽略 dist 下所有文件

/dist

# local env files 忽略脚手架生成的文件

.env.local
.env.\*.local

# Log files 忽略日志文件

npm-debug.log*
yarn-debug.log*
yarn-error.log*
pnpm-debug.log*

# Editor directories and files 忽略编辑器配置文件

.idea
.vscode
_.suo
_.ntvs\*
_.njsproj
_.sln
\*.sw?
```
