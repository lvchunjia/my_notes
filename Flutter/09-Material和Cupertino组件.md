# Material和Cupertino组件

[linwu](https://www.coding-time.cn/)2023年7月9日大约 3 分钟

------

此页内容

- [Flutter Material Design组件](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#flutter-material-design组件)
- - [1. AppBar组件](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#_1-appbar组件)
  - [2. FloatingActionButton组件](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#_2-floatingactionbutton组件)
  - [3. Card组件](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#_3-card组件)
- [Flutter Cupertino风格组件](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#flutter-cupertino风格组件)
- - [1. CupertinoNavigationBar组件](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#_1-cupertinonavigationbar组件)
  - [2. CupertinoButton组件](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#_2-cupertinobutton组件)
  - [3. CupertinoAlertDialog组件](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#_3-cupertinoalertdialog组件)
- [参考资料](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#参考资料)

在本篇文章中，我们将使用官方最新的Dart语法和新知识，详细介绍Flutter中的Material Design和Cupertino风格组件。Flutter提供了两种主题风格，分别是Material Design和Cupertino，用于创建漂亮、一致的用户界面。我们将深入探讨这两种风格的组件，并提供官方文档链接，以便你进一步学习。

## [#](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#flutter-material-design组件)Flutter Material Design组件

Material Design是一种现代化、美观的设计风格，由Google提出，用于创建一致的用户界面。Flutter提供了许多Material Design风格的组件，用于构建漂亮、具有响应性的应用程序。

### [#](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#_1-appbar组件)1. AppBar组件

`AppBar`是Material Design风格的应用栏，通常位于页面的顶部，用于显示标题、操作按钮等。

```dart
AppBar(
  title: Text('My App'),
  actions: [
    IconButton(
      icon: Icon(Icons.settings),
      onPressed: () {
        // 打开设置页面
      },
    ),
  ],
)
```

了解更多：[AppBar组件文档open in new window](https://api.flutter.dev/flutter/material/AppBar-class.html)

### [#](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#_2-floatingactionbutton组件)2. FloatingActionButton组件

`FloatingActionButton`是一个浮动的圆形按钮，常用于触发应用程序中的主要操作。

```dart
FloatingActionButton(
  onPressed: () {
    // 执行操作
  },
  child: Icon(Icons.add),
)
```

了解更多：[FloatingActionButton组件文档open in new window](https://api.flutter.dev/flutter/material/FloatingActionButton-class.html)

### [#](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#_3-card组件)3. Card组件

`Card`是一种具有阴影效果的卡片式容器，常用于显示相关的内容，如图片、标题和描述。

```dart
Card(
  child: Column(
    children: [
      Image.network('https://example.com/image.jpg'),
      ListTile(
        title: Text('Title'),
        subtitle: Text('Description'),
      ),
    ],
  ),
)
```

了解更多：[Card组件文档open in new window](https://api.flutter.dev/flutter/material/Card-class.html)

以上只是一些常用的Material Design组件示例，Flutter提供了更多丰富的组件和功能，你可以根据需要选择适当的组件来构建漂亮的用户界面。

## [#](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#flutter-cupertino风格组件)Flutter Cupertino风格组件

Cupertino是iOS风格的设计语言，Flutter提供了一系列的Cupertino风格组件，使得应用程序可以在iOS设备上具有原生的外观和行为。

### [#](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#_1-cupertinonavigationbar组件)1. CupertinoNavigationBar组件

`CupertinoNavigationBar`是Cupertino风格的导航栏，通常位于页面的顶部，用于显示标题、操作按钮等。

```dart
CupertinoNavigationBar(
  middle: Text('My App'),
  trailing: CupertinoButton(
    child: Icon(CupertinoIcons.settings),
    onPressed: () {
      // 打开设置页面
    },
  ),
)
```

了解更多：[CupertinoNavigationBar组件文档open in new window](https://api.flutter.dev/flutter/cupertino/CupertinoNavigationBar-class.html)

### [#](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#_2-cupertinobutton组件)2. CupertinoButton组件

`CupertinoButton`是Cupertino风格的按钮，具有iOS风格的外观和触摸反馈。

```dart
CupertinoButton(
  onPressed: () {
    // 执行操作
  },
  child: Text('Click Me'),
)
```

了解更多：[CupertinoButton组件文档open in new window](https://api.flutter.dev/flutter/cupertino/CupertinoButton-class.html)

### [#](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#_3-cupertinoalertdialog组件)3. CupertinoAlertDialog组件

`CupertinoAlertDialog`是Cupertino风格的对话框，用于显示警告、确认或其他相关信息。

```dart
showDialog(
  context: context,
  builder: (BuildContext context) {
    return CupertinoAlertDialog(
      title: Text('Alert'),
      content: Text('This is an alert dialog.'),
      actions: [
        CupertinoDialogAction(
          child: Text('OK'),
          onPressed: () {
            // 处理按钮点击事件
            Navigator.of(context).pop();
          },
        ),
      ],
    );
  },
)
```

了解更多：[CupertinoAlertDialog组件文档open in new window](https://api.flutter.dev/flutter/cupertino/CupertinoAlertDialog-class.html)

这些只是一些常用的Cupertino风格组件示例，Flutter提供了更多丰富的组件和功能，你可以根据需要选择适当的组件来构建具有iOS风格的用户界面。

## [#](https://www.coding-time.cn/dart/flutter/Material和Cupertino组件.html#参考资料)参考资料

要深入了解Flutter中的Material Design和Cupertino风格组件，可以参考以下官方资源和文档：

- [Flutter官方文档open in new window](https://flutter.dev/docs)
- [Material Design组件文档open in new window](https://flutter.dev/docs/development/ui/widgets/material)
- [Cupertino风格组件文档open in new window](https://flutter.dev/docs/development/ui/widgets/cupertino)
- [Flutter Cookbookopen in new window](https://flutter.dev/docs/cookbook)

[在 GitHub 上编辑此页open in new window](https://github.com/linwu-hi/coding-time/edit/main/docs/dart/flutter/Material和Cupertino组件.md)