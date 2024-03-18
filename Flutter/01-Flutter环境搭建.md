

[Flutter Version Manager (FVM): Flutter的版本管理终极指南_flutter版本管理工具-CSDN博客](https://blog.csdn.net/qq_28550263/article/details/136300307)

## flutter 多版本管理 fvm

fvm 通过引用每个项目使用的 Flutter SDK 版本来帮助满足一致的应用程序构建的需求。它还允许您安装多个 Flutter 版本，以便使用您的应用程序快速验证和测试即将发布的 Flutter 版本，而无需每次都等待 Flutter 安装

fvm 可以两种模式使用 全局/虚拟环境

### 为啥使用fvm

- 不同的项目可能同时需要多个 Flutter SDK。
- 测试新的 SDK 功能需要在Channels之间切换。
- 版本切换很慢，每次都需要重新安装。
- 无法保持应用程序中 SDK 的最新工作/使用版本。
- Flutter 更新会影响所有 Flutter 项目。
- 团队中开发人员之间的开发环境不一致。

### 安装 fvm

- [从 GitHub 存储库下载](https://link.juejin.cn/?target=https%3A%2F%2Fgithub.com%2Fleoafarias%2Ffvm%2Freleases)
- Windows下通过choco包管理器安装

```shell
# 安装
choco install fvm
```

- Mac OS X/Linux下通过Homebrew包管理器安装

```shell
# 安装
brew tap leoafarias/fvm
brew install fvm
# 卸载
brew uninstall fvm
brew untap leoafarias/fvm
```



### fvm配置

- 环境变量配置

  - 安装fvm后，设置环境变量 FVM_HOME 或 FVM_GIT_CACHE

  ```shell
  # 以mac为例
  # 如果不设置，默认的 flutter SDK 缓存路径为 ~/fvm/versions
  # ~/.zshrc
  export FVM_CACHE_PATH="$HOME/.fvm"
  # 全局flutter 配置（default为切换后的flutter版本软链接）
  export PATH=$HOME/.fvm/default/bin:$PATH
  # 常规flutter 配置
  export PUB_HOSTED_URL=https://pub.flutter-io.cn
  export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn
  ```

IDE配置

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

  - preferences-》Flutter-》Flutter SDK path （填写绝对路径）
    - 全局模式：/Users/mac/.fvm/default
    - 虚拟环境模式（项目中所有的flutter命令需要用 fvm flutter替换）：/项目根目录绝对路径/.fvm/flutter_sdk

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

# 在程序根目录设置flutter版本
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

**fvm install xxx 报错**

```shell
Exception: Git clone failed
```













> 作者：woodwen
> 链接：https://juejin.cn/post/7219130999685611580
> 来源：稀土掘金
> 著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。













