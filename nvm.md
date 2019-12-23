# nvm 介绍及使用

#### nvm是什么？

`nvm`全名`node.js version management`，顾名思义是一个`nodejs`的版本管理工具。通过它可以安装和切换不同版本的`nodejs`。下面列出下载、安装及使用方法。

#### 下载

可在点此在[github](https://github.com/coreybutler/nvm-windows/releases)上下载最新版本,本次下载安装的是`windows`版本。打开网址我们可以看到有两个版本：

- `nvm-noinstall.zip`：绿色免安装版，但使用时需进行配置。

- `nvm-setup.zip`：安装版，推荐使用。

#### 安装

- 1、双击安装文件 `nvm-setup.exe`；
![demo](https://img2018.cnblogs.com/blog/775046/201904/775046-20190411160657751-1529010875.png)
- 2、选择`nvm`安装路径；
![demo](https://img2018.cnblogs.com/blog/775046/201904/775046-20190411160816834-99504468.png)
- 3、选择`nodejs`路径；
![demo](https://img2018.cnblogs.com/blog/775046/201904/775046-20190411161045308-1947410693.png)
- 4、确认安装即可；
![demo](https://img2018.cnblogs.com/blog/775046/201904/775046-20190411171705646-891139870.png)
- 5、安装完确认。
按下`win+r`键，打开`CMD`命令窗口，输入命令 `nvm` ，安装成功则如下显示。可以看到里面列出了各种命令，本节最后会列出这些命令的中文示意。
![demo](https://img2018.cnblogs.com/blog/775046/201904/775046-20190411172641876-1326770838.png)

#### 安装/管理node.js

- 1、查看本地安装的所有版本；有可选参数`available`，显示所有可下载的版本。

```node
nvm list [available]
```

- 2、安装，命令中的版本号可自定义，具体参考命令1查询出来的列表。

```node
nvm install 12.14.0
```

- 3、使用特定版本。

```node
nvm use 12.14.0
```

- 4、卸载。

```node
nvm uninstall 12.14.0
```

#### 命令提示

- 1、`nvm arch` ：显示`node`是运行在32位还是64位。
- 2、`nvm install <version> [arch]` ：安装`node`， `version`是特定版本，也可以是最新稳定版本`latest`。可选参数`arch`指定安装32位还是64位版本，默认是系统位数。可以添加`--insecure`绕过远程服务器的SSL。
- 3、`nvm list [available]` ：显示已安装的列表。可选参数`available`，显示可安装的所有版本。`list`可简化为`ls`。
- 4、`nvm on` ：开启`node.js`版本管理。
- 5、`nvm off` ：关闭`node.js`版本管理。
- 6、`nvm proxy [url]` ：设置下载代理。不加可选参数`url`，显示当前代理。将`url`设置为`none`则移除代理。
- 7、`nvm node_mirror [url]` ：设置`node`镜像。默认是`https://nodejs.org/dist/`。如果不写`url`，则使用默认`url`。设置后可至安装目录`settings.txt`文件查看，也可直接在该文件操作。
- 8、`nvm npm_mirror [url]` ：设置`npm`镜像。`https://github.com/npm/cli/archive/`。如果不写`url`，则使用默认`url`。设置后可至安装目录`settings.txt`文件查看，也可直接在该文件操作。
- 9、`nvm uninstall <version>` ：卸载指定版本`node`。
- 10、`nvm use [version] [arch]` ：使用制定版本`node`。可指定32/64位。
- 11、`nvm root [path]` ：设置存储不同版本`node`的目录。如果未设置，默认使用当前目录。
- 12、`nvm version` ：显示`nvm`版本。`version`可简化为v。

<font color="red">注：安装路径最好不要出现中文和空格。</font>
