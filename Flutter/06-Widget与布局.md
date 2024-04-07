> Flutter的布局与HTML/CSS布局方式上的写法有很大的不同，Flutter使用基于组件树的布局模型，其中每个组件都有自己的布局和渲染逻辑。相比之下，HTML/CSS使用基于盒模型的布局，其中元素通过框模型和定位属性进行布局。



## 一、Widget

在Flutter中，一切皆是Widget。Widgets是Flutter用户界面的基本构建块，用于描述应用程序在给定其当前配置和状态的情况下应该如何显示。通过组合不同的Widget，我们可以构建出复杂、美观的用户界面。

Flutter中的Widget分为两类：

### 1. StatelessWidget

`StatelessWidget` 是抽象类，继承自 `Widget` 。本身的源码是非常简单的，其中只有一个 `build` 抽象方法用来构建组件，进行返回。也就是说，`StatelessWidget` 的派生类必须实现 `build` 方法，返回组件。

`StatelessWidget` 是不可变的，一旦创建就不能更改。它们通常用于表示那些没有状态改变的静态UI元素。例如，`Icon`、`Text`、`Container`等都是无状态的Widget。

```dart
class MyStatelessWidget extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Container(
      child: Text('Hello World'),
    );
  }
}
```

### 2. StatefulWidget

`StatefulWidget`是有状态的，可以根据应用程序的状态和用户交互来改变。当状态发生变化时，`StatefulWidget`会自动重绘 UI 。常见的有状态Widget包括按钮、输入框、列表等。

```dart
class MyStatefulWidget extends StatefulWidget {
  @override
  _MyStatefulWidgetState createState() => _MyStatefulWidgetState();
}

class _MyStatefulWidgetState extends State<MyStatefulWidget> {
  bool _isPressed = false;

  @override
  Widget build(BuildContext context) {
    return RaisedButton(
      onPressed: () {
        setState(() {
          _isPressed = !_isPressed;
        });
      },
      child: Text(_isPressed ? 'Pressed' : 'Not Pressed'),
    );
  }
}
```

`StatefulWidget` 继承自 `Widget` 的抽象类，其中定义了 `createState` 抽象方法，返回 `State` 对象。`State` 是一个抽象类，其中只有一个 `build` 抽象方法，返回 `Widget` 对象

对于 `Widget` 来说，有个约定：`所有组件的成员属性必须是不可变的` ，也就是说都需要通过 `final` 进行修饰。无论任何 `Widget` 的衍生类都是如此，即便是 `StatefulWidget` 一族组件 。`Flutter` 框架中 `Widget` 只作为对界面结构的配置描述，一旦一个 `Widget` 对象创建之后，就不允许对其成员属性进行任何修改。这本质上是 `final` 关键字的限制。

想要更新界面中文字的内容，唯一的方式就是给出新的配置信息，改变文字对象。又因为 `Widget` 派生类不允许修改任何成员，所以修改数据的过程就无法在 `Widget` 派生类中完成。这就是 `State` 类诞生的原由：我们需要有一处地方，可以修改数据，并触发重新构建界面的逻辑，实现界面更新。



## 二、布局组件

### 0. 布局的重点：约束

约束是 `Flutter` 布局的 `独有特性` ，也是对布局来说`最`为重要的概念。约束，就是`限制条件`。 那么`Flutter` 的约束 `限制的是什么` 。

`Flutter `中的约束通过 `Constraints` 类进行抽象，其中只有 `BoxConstraints` 和 `SliverConstraints` 两种实现类。 `SliverConstraints` 是在滑动中的约束，非滑动组件中的约束指的都是盒约束 `BoxConstraints`。

```dart
class BoxConstraints extends Constraints {
  /// Creates box constraints with the given constraints.
  const BoxConstraints({
    this.minWidth = 0.0,
    this.maxWidth = double.infinity,
    this.minHeight = 0.0,
    this.maxHeight = double.infinity,
  });
}
```

从上面 `BoxConstraints` 定义中可以看出，其本质就是维护 `宽高 `两个维度的 `范围`。`父级传递约束` 就是用来 `确定子级尺寸 `的，另外约束在布局中的一大特点是 `传递性`。

对与父子孙三级组件，子所 `受到的约束` 是由 `父` 传递的。该约束会用来确定 `子` 的尺寸，并且不同组件确定尺寸的逻辑不同，这个逻辑就是其布局的 `尺寸特性`。

同理，`子` 会也会传给 `孙` 一个约束，用于限制 `孙` 的尺寸，并且不同组件确定传递约束的逻辑不同，这个逻辑就是其布局的 `约束特性`。

`尺寸` 和 `约束` 是所有布局组件都会有的特性，至于偏移量，只有某些组件会有。比如 `Align` 、`Padding` 等，可以让子级相对于区域左上角产生偏移。



### 1. Container

Container是一个多功能的容器，可以用于装饰、定位和约束其子Widget。你可以设置它的大小、颜色、边距等。

```dart
Container(
  color: Colors.blue,
  width: 200,
  height: 200,
  child: Text('Hello'),
)
```

### 2. Row和Column

Row和Column是用于水平和垂直排列子Widget的强大布局组件。你可以在它们内部添加各种子Widget，并使用`mainAxisAlignment`和`crossAxisAlignment`来调整对齐方式。

```dart
Row(
  mainAxisAlignment: MainAxisAlignment.center,
  crossAxisAlignment: CrossAxisAlignment.center,
  children: <Widget>[
    Icon(Icons.star),
    Icon(Icons.star),
    Icon(Icons.star),
  ],
)
```

### [#](https://www.coding-time.cn/dart/flutter/Widget.html#stack)**Stack**

Stack允许将多个子Widget堆叠在一起，可以通过定位、对齐和尺寸调整来控制它们的位置。

```dart
Stack(
  alignment: Alignment.center,
  children: <Widget>[
    Container(color: Colors.red, width: 200, height: 200),
    Container(color: Colors.green, width: 150, height: 150),
    Container(color: Colors.blue, width: 100, height: 100),
  ],
)
```

### [#](https://www.coding-time.cn/dart/flutter/Widget.html#listview)**ListView**

ListView是一个滚动视图，可用于显示可滚动的列表。你可以使用`ListView.builder`或`ListView.separated`来构建列表。

```dart
ListView.builder(
  itemCount: 100,
  itemBuilder: (context, index) {
    return ListTile(
      title: Text('Item $index'),
    );
  },
)
```

### [#](https://www.coding-time.cn/dart/flutter/Widget.html#expanded)**Expanded**

Expanded是一个灵活的布局组件，用于占据剩余可用空间。它通常与Row和Column一起使用。

```dart
Row(
  children: <Widget>[
    Expanded(
      child: Container(color: Colors.red),
    ),
    Expanded(
      child: Container(color: Colors.green),
    ),
  ],
)
```

这只是布局组件中的几个例子，Flutter提供了丰富的布局组件，适应各种不同的UI需求。你可以根据需要选择合适的布局组件。

更多关于布局的内容，你可以参考[Flutter布局指南open in new window](https://flutter.dev/docs/development/ui/layout)。

















