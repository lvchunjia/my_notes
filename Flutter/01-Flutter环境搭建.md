

## 一、Flutter SDK安装

### dart SDK下载与安装

*注意：fluttersdk默认带有dart，若无需使用命令行等执行dart文件则无需单独安装dart*

下载：

- [Dart 英文文档](https://dart.dev/)
- [Dart 中文文档 | Dart](https://dart.cn/)

### FlutterSDK 的下载与安装

下载 FlutterSDK：

- [flutter英文官网]([Flutter SDK archive | Flutter](https://docs.flutter.dev/release/archive?tab=macos))

- [Flutter中文]([Using Flutter in China | Flutter](https://docs.flutter.dev/community/china))

下载完后，解压到一个文件夹下

### 配置环境变量

将 `flutter\bin` 文件夹路径配置到 Path 环境变量中。

在系统变量中配置官方提供的国内镜像

```bash
PUB_HOSTED_URL=https://pub.flutter-io.cn
FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
```

执行 `flutter --version`，能给出结果，说明 Flutter 环境配置成功



## 二、多版本管理： fvm

> 参考：[ flutter版本管理工具-CSDN博客](https://blog.csdn.net/qq_28550263/article/details/136300307)、[flutter 多版本管理 fvm-稀土掘金](https://juejin.cn/post/7219130999685611580)

### 什么是FVM？

fvm 通过引用每个项目使用的 Flutter SDK 版本来帮助满足一致的应用程序构建的需求。它还允许您安装多个 Flutter 版本，以便使用您的应用程序快速验证和测试即将发布的 Flutter 版本，而无需每次都等待 Flutter 安装

fvm 可以两种模式使用 全局/虚拟环境

### 为什么使用fvm

- 版本隔离
  它允许为每个项目维护独立的 Flutter 版本，从而避免了不同项目之间可能出现的版本冲突问题。由于不同的项目可能依赖于不同的 Flutter 版本，版本隔离确保了项目之间的独立性，使得开发者可以根据项目的需要选择合适的 Flutter 版本进行开发和测试，而无需担心可能会因为版本不匹配而导致的问题。
- 快速切换
  通过简单的命令，开发者可以在不同的项目之间快速切换 Flutter 版本，而无需手动管理不同版本的 Flutter SDK，大大提高了开发效率和便捷性。
- 节省空间
  由于 FVM 允许共享相同版本的 Flutter SDK，并且只需下载一次即可在多个项目中使用，因此可以避免重复下载相同版本的 Flutter SDK，从而节省了存储空间。



### 安装 fvm

- [从 GitHub 存储库下载](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fleoafarias%2Ffvm%2Freleases)
- 通过 pub 安装：`dart pub global activate fvm`

#### Mac安装 fvm

- Mac OS X/Linux下通过Homebrew包管理器安装

```shell
# 安装
brew tap leoafarias/fvm
brew install fvm
# 卸载
brew uninstall fvm
brew untap leoafarias/fvm
```

安装完成后执行 `fvm--version` 检查是否成功

**fvm环境变量配置**

安装fvm后，设置环境变量

```shell
# 以mac为例 ~/open .zshrc 打开脚本配置，添加
# 可选：默认的 flutter SDK 缓存路径为 ~/fvm/versions
export FVM_CACHE_PATH="$HOME/.fvm"
# 全局flutter 配置（default为切换后的flutter版本软链接） 若以上未修改，则为将.fvm换为fvm
export PATH=$HOME/.fvm/default/bin:$PATH
```

#### Win安装fvm

- windows 下安装Chocolatey（强大的软件包管理工具）

```shell
Set-ExecutionPolicy Bypass -Scope Process -Force; iex ((New-Object System.Net.WebClient).DownloadString('https://chocolatey.org/install.ps1'))
```

- 使用choco安装fvm

```shell
choco install fvm
```



### 使用前设置

- 配置完环境变量后安装flutter并设为默认

```shell
# 安装最新版稳定flutter版本
fvm install stable
# 设置为全局
fvm global stable
```

- 可选：flutter 国内镜像（flutter中文开源社区镜像，也可选其它）

```shell
export PUB_HOSTED_URL=https://pub.flutter-io.cn
export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
```



### 常用命令

```shell
# 查看现有远程版本
fvm releases list
# 安装flutter版本
fvm install 3.7.10
# 卸载flutter版本
fvm remove 3.7.10
# 查看本地已装的版本
fvm list installed versions
# 在程序根目录设置项目的flutter版本
fvm use 3.7.10
# 设置全局版本
fvm global 3.7.10
# 项目目录下执行，可获取当前的使用版本
fvm list
# 在当前项目目录下执行，可获取当前项目的flutter版本
fvm flutter --version
# 在当前项目目录下执行，清理项目缓存
fvm flutter clean
# 在当前项目目录下执行，获取依赖包
fvm flutter pub get
# 在当前项目目录下执行，项目运行
fvm flutter run
```

### 配置git忽略

在配置了fvm以后，在.fvm目录下会有一个flutter_sdk的链接文件，这个文件是不需要上传git的，否则会有冲突，在.gitignore文件中过滤一下。

```bash
/.fvm/flutter_sdk
```

### IDE配置

- vscode

  - 可全局配置 vscode（～/Library/Application\ Support/Code\ -\ Insiders/User/settings.json）

    ```shell
    # 以mac为例
    {
        "dart.flutterSdkPaths": [
            "/Users/usr/fvm/versions/stable",
            "/Users/usr/fvm/versions/dev"
        ]
    }
    # 然后在 vscode 控制面板中执行 Flutter: Change SDK 切换 Flutter SDK 版本，
    # 将同步记录到当前项目的 vscode 配置文件 .vscode/settings.json 中（dart.flutterSdkPath）
    ```

  - 也可直接编辑当前项目的 vscode 配置文件 .vscode/settings.json

    ```shell
    # 以mac为例
    {
        "dart.flutterSdkPath": ".fvm/flutter_sdk",
        # or "dart.flutterSdkPaths": [".fvm/flutter_sdk"]
        
        # Remove .fvm files from search
        "search.exclude": {
            "**/.fvm": true
        },
        # Remove from file watching
        "files.watcherExclude": {
            "**/.fvm": true
        }
    }
    ```

- android studio

  - preferences ==》Flutter ==》Flutter SDK path （填写绝对路径）
    - 全局模式：/Users/mac/fvm/default
    - 虚拟环境模式（项目中所有的flutter命令需要用 fvm flutter替换）：/项目根目录绝对路径/fvm/flutter_sdk

### 常见问题解决

**`brew install fvm`报错解决**

```shell
➜  ~ brew install fvm
==> Fetching leoafarias/fvm/fvm
==> Downloading https://storage.googleapis.com/dart-archive/channels/stable/release/3.2.6/sdk/dartsdk-macos-arm64
curl: (35) Recv failure: Connection reset by peer

Error: fvm: Failed to download resource "fvm--dart-sdk"
Download failed: https://storage.googleapis.com/dart-archive/channels/stable/release/3.2.6/sdk/dartsdk-macos-arm64-release.zip
```

即使开了vpn，通过Homebrew下载依然会报错，因为终端默认不会走代理，通过在终端执行以下命令，将终端修改为走代理路径即可。

注意：

- 需将下方命令的端口修改为你的代理端口
- 该命令只在本次终端开启期间生效，重启终端后将失效（不建议永久修改）

```shell
export http_proxy=http://127.0.0.1:15732 https_proxy=http://127.0.0.1:15732

export http_proxy=http://127.0.0.1:15732 https_proxy=http://127.0.0.1:15732
git config --global https.proxy https://127.0.0.1:15732
git config --global https.proxy http://127.0.0.1:15732
```

配置环境变量到脚本工具中: 由于mac的脚本工具有 `.bash` 和 `.zsh` 两个，一般默认的是 bash，具体切换，[可以在这里参看苹果官网的切换方法](https://link.juejin.cn?target=https%3A%2F%2Fsupport.apple.com%2Fzh-cn%2FHT208050)

- 如果是`.bash`作为默认Shell,可以在终端中使用 `open -e .bash_profile` 命令打开文件
- 如果是`.zsh`作为默认Shell，可以在终端中使用 `open .zshrc` 命令打开文件

**`fvm install xxx` 报错**

```shell
Exception: Git clone failed
```

若install时报错且设置终端代理以及git代理地址都不生效，可尝试切换fvm安装方式

本人使用Homebrew安装后install报错如上，切换为dart pub安装后可正常使用





## 三、Android Studio开发Flutter

### 1. 快捷键

1. 快速创建Widget：在dart文件中输入`stf`或`stl`出现提示后按回车即可  
1. 快速修复：`command + .`
1. 自动生成构造函数：选中 final 参数，快捷键：`option + 回车`
1. 添加父组件、变为子组件、删除子组件：`option+回车`
1. 万能的搜索：双击shift
1. 查看最近打开的文件：`command + E`
1. 重命名：`fn+shift+f6`
1. 查看当前类结构：`command + fn + f12`
1. 查看源码：将光标放到要查看源码的类名或方法名上，长按command 然后的点击  
1. 查看类的子类：选中要查看的类，然后：`command + B` 或 `option + command + B`
1. 将代码更新到模拟器上：选中模拟器然后 `command + R`
1. 导入类的快捷键：将光标放在要导入类的上面，然后按 `option + enter`
1. 前进后退：当跟踪代码的时候，经常跳转到其他类，后退快捷键：`option+command+方向左键`，前进快捷键：`option+command+方向右键`
1. 全局搜索：`command + shift + F`
1. 全局替换：`command + shift + R `
1. 查找引用： `option + shift + F7`  

> 以上快捷键是在Android Studio 的macOS的keymap下，如果是Windows系统，将command 换成Ctrl，option 换成 Alt即可。



### 2. 提取Flutter代码

Flutter最让人头疼的一点是的布局的嵌套，对于复杂的布局如果不进行任何重构的情况下会嵌套的非常深，从而降低代码的可读性不利于后期的维护。

推荐的做法是将复杂的布局提取成一个函数或者一个组件，选中一个比较复杂的widget，鼠标右键进入 Refactor > Extract Method ，然后给这个方法取一个名字，AS 可以自动把这块代码抽离出一个`Method`并为它添加参数。

除此之外，我们还可以借助AS来将符合条件的代码块提取成一个Widget，只需要在Refactor中选择 Extract Flutter Widget即可。



### 3. 代码自动格式化

虽然我们可以通过快捷键`option(alt)+command(ctrl)+L`来在提交代码是格式化，但是这种手动的方式显然不够效率。下面我们来借助AS的保存时代码自动格式化功能来释放我们的双手：在 Settings > Language & Frameworks > Flutter 中选上 "Format Code on Save"这个选项



## 四、VS Code开发Flutter

### 1. 快捷键

1. 快速创建Widget：在dart文件中输入stf或stl出现提示后按回车即可  
2. 快速修复：command + .  
3. 自动生成构造函数：选中 final 参数，快捷键：command + .  
4. 添加父组件、变为子组件、删除子组件：command + .  
5. 重新打开 关闭的编辑页面：command + shift + T  
6. 通过匹配文本打开文件：command + T  
7. 代码格式化：shift + option + F  
8. 打开console ：command + J  
9. 查看源码：将光标放到要查看源码的类名或方法名上，长按command 然后的点击  
10. 查看类的子类：选中要查看的类，然后：command + F12  
11. 后退：当跟踪代码的时候，经常跳转到其他类，后退快捷键：ctrl + -  
12. 导入类的快捷键：将光标放在要导入类的上面，然后按 command + .  
13. 全局搜索：command + shift + F  
14. 把当前行代码和上一行/下一行代码互换位置：option + 上↑/下↓  
15. 快速复制当前行：option + shift + 下↓  



### 2. 运行项目相关命令

```bash
flutter run: 运行当前连接设备  
flutter run -d 设备id：运行指定设备  
  
运行项目后：  
q：终止运行  
r：热重载  
command + k ：清除终端输出的信息  
flutter clean ：清理缓存，可用于更改代码后运行有些异常，的一种处理方式。  
flutter --version ： 查看 Flutter 版本  
```



### 3. 提取Flutter代码

选中一个比较复杂的widget，然后通过快捷键 `command + .` Refactor > Extract Method ，然后给这个方法取一个名字，VS Code 可以自动把这块代码抽离出一个`Method`并为它添加参数











































