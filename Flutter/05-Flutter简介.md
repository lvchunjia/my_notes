



# 一、Flutter简介

Flutter是由Google开发和维护的开源框架，自2017年以来，已经迅速获得了开发者社区的广泛认可。其主要目的是开发出高性能、高保真的移动应用程序，用于iOS和Android两个主要平台。

Google创建Flutter的初衷是解决跨平台开发中的一些普遍问题，包括性能瓶颈，不同平台的UI不一致等。Google希望Flutter能够创建美观、流畅且用户体验接近原生应用的应用程序。目前，Flutter已经逐步扩展到其他平台，如Web、桌面应用和嵌入式系统。

## 1. Flutter架构

Flutter框架的架构设计主要分为三层：

1. **框架层**：框架层是基于Dart语言实现的，并为开发者提供了丰富的API。它主要包括Material和Cupertino两种设计风格的Widget，各种布局方式（Stack, Row, Column等），以及用于处理交互（手势处理，动画，路由/导航）的API。
2. **引擎层**：引擎层主要是用C++编写的，并提供了低级别的服务，如网络、存储、插件的支持。此外，还包括Dart运行时环境以及Skia图形渲染引擎。
3. **嵌入层**：嵌入层是特定于平台的，负责在各种不同的操作系统上启动Flutter应用。这一层包括Android和iOS的嵌入API，用于将Flutter引擎加载到Android和iOS应用程序中。

## 2. Flutter与Dart

Flutter选择了Dart作为其开发语言。这主要有以下几个原因：

1. **性能**：Dart支持Ahead-Of-Time（AOT）编译，即预编译，可以将Dart代码直接编译为本地机器码，这对于提高Flutter应用的启动速度和运行性能至关重要。
2. **热重载**：Dart也支持Just-In-Time（JIT）编译，即边编译边执行，这意味着开发者可以在应用程序运行过程中进行修改并立即看到结果，这极大地提高了开发效率。
3. **易学易用**：Dart语法简洁明了，对于大多数开发者来说，特别是具有Java或JavaScript背景的开发者，能够轻松地上手Dart。
4. **单语言开发**：使用Dart，开发者可以同时编写前端界面和后端逻辑，无需切换不同的语言，这有助于提高开发效率。
5. **垃圾收集和内存管理**：Dart语言的这些特性有助于简化开发流程，同时提高应用的运行效率。

总的来说，Flutter框架提供了一个全新的方式来构建和部署跨平台的UI驱动型应用，而Dart语言则为其提供了强大的后盾，使得Flutter应用能够有出色的性能，同时还具有快速开发的能力。



# 二、第一个Flutter应用

## 1. 创建 Flutter 项目

在命令行或终端中，进入你希望创建项目的目录，并执行以下命令来创建一个新的Flutter项目：

```bash
flutter create hello_world_app
```

这将会创建一个名为`hello_world_app`的新目录，其中包含Flutter项目的初始结构。

## 2. 运行应用

回到命令行或终端，确保你仍然在`hello_world_app`目录下。执行以下命令来运行你的应用程序：

```bash
flutter run
```

这将会在连接的设备或模拟器上启动你的Flutter应用程序。

项目运行之后，可以看到模拟器上展示了一个计数器应用，随着点击右下角的按钮，中间的数字会进行自加。这就是默认的计数器项目。

## 3. 项目结构

### 3.1. 各平台文件夹

六个平台的项目包，其中每个包都是独立的项目。 `Flutter` 的价值在于为各平台项目提供统一的界面交互，并构建各平台可运行的应用产物。

`Flutter` 本身是六个项目的集合体，使用各平台开发的 `IDE` 可以单独运行相关平台项目。`Flutter` 本质上是以一种 `三方库` 的形式，集成在平台中，提供界面表现的一种技术。只不过 `Flutter` 可以使用 `Dart` 语言进行逻辑处理，就有种`“反客为主”`的感觉。一般而言，对于应用程序，最重要的功能就是界面的呈现与交互，所以可以说 `Flutter` 抢了各平台原生视图的`“饭碗”`。

而各个平台抛除 `视图呈现` 之外，只剩下一些平台的特殊功能。比如蓝牙连接、电池电量、音视频解码、数据库操作等。这些虽然可以由 `平台项目` 提供功能，但为了功能的独立性和可复用性，一般使用 `插件` 的形式提供功能。这种 `“可插拔”` 的方式集成功能，也是编程思维的一种体现形式。所以这就导致：`Flutter` 项目中的平台项目，一般只起到构建配置的作用，比如权限、运行设备最低版本、应用图标、名称等，而不承担代码编写的职能。

## 4. lib 文件夹

`Flutter` 对于界面的构建代码集中在 `lib` 文件夹中，这里 `main.dart` 文件中的代码，决定着运行时应用的界面表现。

序的入口文件可以进行修改，在 `AndroidStudio` 中，点击 `Edit Configurations...` 可以弹出运行相关的配置界面，在 `Dart entrypoint` 栏可以选择对应的 `main.dart` 入口文件。

## 5. pubspec.yaml 文件

这个文件用于对项目进行配置，其中 `name` 表示项目名称，值得注意一点：在使用项目绝对路径时，`"package:idream"` 中的 `idream` 就是由这个字段确定的。也就是说，当这个名称改变时，项目中所有的绝对路径方式 `"import"` 的语句都会出错。

在 `dependencies` 节点下可以引入三方依赖库，这对于开发者而言是非常重要的。毕竟很多公共的基础功能并不需要从零开始，比如网络访问、数据库支持、分享等。可以通过引入三方库，借助别人的力量，站在巨人的肩膀上。这就是一项技术 `“生态”` 的重要一环，最常用的仓库是 [【pub.dev】](https://pub.dev/) ，访问不了的话，也可以用中文镜像 [【pub.flutter-io.cn】](https://pub-web.flutter-io.cn/)。

最后一段是资源文件的配置，比如一些图片、字体、文本等静态资源，需要配置之后才能访问。一般而言，我们会在根目录下新建一个 `assets` 文件夹用于盛放这些资源文件。但这并不是强制性的，只要资源配置时路径填写正确即可。

```dart
name: idream # 项目名称
description: A dream start of Flutter. # 描述信息
publish_to: 'none' # 是应用程序，不是发布到 pub 的三方库，这里填 none 
version: 1.0.0+1 # 应用版本

environment:
  sdk: ">=2.17.0 <3.0.0" # Dart SDK 适用版本范围

dependencies:
  flutter:
    sdk: flutter
  cupertino_icons: ^1.0.2

dev_dependencies:
  flutter_test:
    sdk: flutter
  flutter_lints: ^1.0.0
    
flutter:
  uses-material-design: true
  assets:
    - assets/images/
    - assets/data/
    - assets/images/head_icon/
    - assets/images/widgets/
    - assets/flutter.db
    - assets/version.json

  fonts: # 配置字体，可配置多个，支持ttf和otf,ttc等字体资源
    - family: CHOPS
      fonts:
        - asset: assets/fonts/CHOPS.TTF
    - family: TolyIcon
      fonts:
        - asset: assets/iconfont/iconfont.ttf
```



# 三、AndroidStudio辅助工具

## 1. 全局搜索

在顶部栏 `Edit/Find/Find in Files` 打开搜索面板，面板中也可以看到对应的快捷键（`shift` + `command` + `f`）。如果快捷键没响应，很大可能是和输入法的快捷键冲突了。比如搜狗输入法，禁用其快捷键即可。

## 2. 类结构信息

当分析一份代码文件时，在 AndroidStudio 中可以打开 `Structure` 页签，其中会展示出当前文件中的所有类的结构信息，比如成员属性、成员方法等。这样，你可以快速了解这份代码有哪些东西，在点击信息时，也能立刻跳转到对应的代码处。

其中 `C` 图标表示类，`m` 图标表示方法， `f` 图标表示成员属性。当前文件夹中定义了三个类型和一个 main 方法。每个类型中会定义若干方法和属性，其中可以清晰地看出函数的名称、入参和返回值。

## 3. 布局分析

在 `Flutter Inspector` 页签中，可以看出当前界面的布局结构。点击某项时，会跳转到代码对应的位置，这就是不过展示布局结构，辅助我们快速定位到对应代码位置。

如果布局结构过于复杂，在树中寻找节点也非常麻烦。如果现在已经有了一个项目，运行起来，如何迅速找到界面中的部件，对应代码中的位置呢？ `Flutter Inspector` 中提供了选择模式。选择模式下，当点击界面上的显示部件，就会自动挑战到对应的代码位置。对于定位代码来说，可谓神器。另外注意一点，点击后左下角会有个搜索按钮，如果想选择其他部件，要先点一下那个搜索按钮



# 四、计数器代码分析

去除注释之后，计数器项目也就 `68 行` 代码，算是一个非常简单的小项目，但它完成了一个基本的功能交互。可谓麻雀虽小五脏俱全。一开始是 `main` 方法，表示程序的入口，其中先创建 `MyApp` 类型对象，并将该对象作为参数传入 `runApp` 函数中。也就是说 `MyApp` 是决定界面显示的类。

```dart
void main() {
  runApp(const MyApp());
}
```



## 1. Widget 类型

`MyApp` 继承自 `StatelessWidget` 类，并覆写了其 `build` 方法，返回 `Widget` 类型对象；在方法的实现中，创建了 `MaterialApp` 对象并返回，其中 `theme` 入参表示主题， 通过 `Colors.blue` 可以看到蓝色主题的来源。

```dart
class MyApp extends StatelessWidget {
  const MyApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Flutter Demo',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const MyHomePage(title: 'Flutter Demo Home Page'),
    );
  }
}
```

决定界面展示的配置信息的类型我们称之为 **组件 Widget**， `runApp` 方法的入参是 `Widget` 类型，而 `MyApp` 可以占位参数，就说明它是 `Widget` 的派生类；`MyApp#build` 方法返回的是 `Widget` 类型，方法实现中实际返回的是 `MaterialApp` 对象，就说明 `MaterialApp` 也是 `Widget` 的派生类。这也是一个简单的逻辑推理过程。

另外 `MaterialApp` 构造方法的 `home` 入参，也是需要传入一个 `Widget` 类型，所以下面的 `MyHomePage` 也是 `Widget` 的派生类。从这里可以看出， Flutter 框架中界面的展示和 `Widget` 一族息息相关。

## 2. MyHomePage 代码分析

`MyHomePage` 继承自 `StatefulWidget` , 其中有一个 `String` 类型的成员属性 `title`，并在构造时进行赋值。另外，还覆写了 `createState` 方法，创建 `_MyHomePageState` 对象并返回。

```dart
class MyHomePage extends StatefulWidget {
  const MyHomePage({super.key, required this.title});

  final String title;

  @override
  State<MyHomePage> createState() => _MyHomePageState();
}
```



















