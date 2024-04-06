



# 一、类和对象

面向对象编程（Object Oriented Programming，简称OOP）是一种编程范型，它使用 "对象"：包含数据字段（属性）和在对象上执行操作的方法。这是一种设计和结构化代码的方式，允许我们创建复杂的应用程序，使用基本代码构建并易于理解和维护。

Dart 作为一种面向对象的类定义语言，使用混合的继承模式：即，Dart 中的类只能有一个超类，但可以实现多个接口。类定义的语法非常接近于 C-style 的语言（如 Java、C++ 和 JavaScript），这使得大多数开发者可以快速理解和学习 Dart。

## 1. 类的定义与实例化

在 Dart 中，我们可以通过 `class` 关键字来定义一个类。类是一种复合的数据类型，即它包含成员方法（函数）和变量（称为"成员属性"）。

```dart
class Person {
  String name;
  int age;

  void sayHello() {
    print('Hello, my name is $name, I am $age years old.');
  }
  
  String getInfo() => "Person($name,$age)";
}
```

创建类的实例（也就是对象），我们可以使用 `new` 关键字，然后调用类的构造函数。在 Dart 2 中，`new` 关键字是可选的：

```dart
var person = Person();
person.name = 'Alice';
person.age = 20;
person.sayHello();
```

我们可以使用 `.` 符号来访问对象的属性和方法：

```dart
print(person.name);  // 输出 Alice
person.sayHello();  // 输出 Hello, my name is Alice, I am 20 years old.
```

## 2. getter和setter方法

我们可以使用 getter 和 setter 方法来读取和写入对象的属性，`get` 与 `set` 关键字修饰的是 `成员方法` ，其实本质上来说它们只是一种简写方式，常用于对 `成员变量` 的维护，它只不过是个语法糖，本质上仍是方法。。通过 `get` 关键字声明的成员方法，在调用时不加 `()` 。



```dart
class Person {
  String name;
  int age;

  String get greeting => 'Hello, my name is $name, I am $age years old.';
  void set setName(String name) => this.name = name;
}

var person = Person();
person.setName = 'Alice';
print(person.greeting);  // 输出 Hello, my name is Alice, I am null years old.
```

## 3. 构造方法

在 Dart 中，构造函数的名称与类的名称相同，我们可以在构造函数中初始化对象的属性，在实例化对象时，会触发函数体的逻辑，对属性进行赋值，这就是**通过构造函数初始化成员属性**。

构造方法作为一种特殊的函数，在定义上有一些独有的特点：

- 构造方法在声明时无 `返回值` 。
- 构造方法 `可以` 没有方法体。
- 在参数列表中可以通过 `this.成员` ，可以为成员变量进行赋值。

```dart
class Person {
  String name;
  int age;

  // 这是一个构造函数
  Person(String name, int age) {
    this.name = name;
    this.age = age;
  }

  void sayHello() {
    print('Hello, my name is $name, I am $age years old.');
  }
}

var person = Person('Alice', 20);
person.sayHello();
```

在构造方法的右括号后可以加 `:` 号，之后添加一些表达式，常用于对成员变量的初始化，多个表达式通过 `,` 号隔开。

```dart
Person(String name, int age)
    : this.name = name,
      this.age = age;
```

上面的构造方法相当于下面写法的简化版，`this` 关键字引用的是当前实例。我们可以在构造函数或其他方法中使用 `this` 关键字来访问当前对象的属性或方法。另外，构造函数中，通过 `this` 对象进行赋值的操作

```dart
class Person {
  String name;
  int age;

  Person(this.name, this.age);
}
```

构造方法中也可以使用 `命名参数`。当成员变量过多时，那按参数顺序进行初始化会比较麻烦。这时 `命名参数` 就会非常方便，因为它可以支持 `参数的乱序` 和 `参数的默认值`。

另外注意一点，对于非空类型的成员，在构造方法中必须进行初始化，而 `命名参数` 是选填的，所以如果没有提供默认值，就必须提供一个解决方案保证该成员被初始化。这就是 `required` 关键字

```dart
class Vec2 {
  double x;
  double y;
  String? name;
  String nickName;

  Vec2(this.x, this.y, {String? name, required this.nickName});
}

Vec2 p0 = Vec2(4, 3 );
Vec2 p0 = Vec2(4, 3,name: "P0");
```

## 4. 命名构造

一个类，可以有多种构造方式，对于 `C++` 和 `Java` 等支持函数重载的语言，可以通过重载进行实现多种构造。但 `Dart` 不支持函数重载，重载特性优劣参半，重载过多会使方法比较混乱。`Dart` 对于多种构造方式有更优雅的方式： `命名构造` 。

```dart
class Vec2 {
  double x;
  double y;

	Vec2.polar(double length, double rad):
      x = length*math.cos(rad),
      y = length*math.sin(rad);
}

Vec2 p1 = Vec2.polar(10, math.pi/4);
print(p1.getInfo()); // Vec2(7.0710678118654755,7.071067811865475)
```

一个类中命名构造的个数不限，只需要通过 `类名.构造名` 就可以定义。

## 5. 私有属性和方法

在 Dart 中，以 `_` 开头的属性和方法是私有的，不能在类的外部访问：

```dart
class Person {
  String _name;
  int _age;

  void _privateMethod() {
    // ...
  }
}
```

在上面的代码中，`_name`、`_age` 和 `_privateMethod` 都是私有的，只能在 `Person` 类内部访问。如果一个成员是私有的，但我们需要访问它，这时可以提供 `get` 方法。这样就可以实现对 `成员变量` 的 `只读` 特性；同理提供 `set` 方法，可以对私有成员进行修改。

另外，对于类本身来说，可见性也具有相同的特点。如果另一个文件中的类，其名称以 `_` 开头，可无法访问该类。这里要特别注意一点：可见性的单位是 `文件` 。同一文件中并没有可见性的区分，也就是说在使用同一文件中的类时，以 `_` 开头的 `类` 、`成员方法` 、`成员变量` 的访问不受限制。

## 6. 类中的不可变成员

类的一个成员变量使用 `final` 进行修饰，就表示这个成员不允许进行修改。如果在类设计时，某个成员变量没有被修改的需求，可以使用 `final` 进行修饰，这样可以避免外界对成员变量的误操作。

```dart
class Vec2 {
  final double x;
  final double y;

  Vec2(this.x, this.y);
}
```

## 7. 静态成员

通过在成员前面加上`static`关键字来定义静态成员。静态成员是属于类本身而不是类的实例的成员，静态成员在类的所有实例之间共享，并且可以通过类名直接访问，无需创建类的实例。

静态成员包括静态变量和静态方法。可以直接通过类名访问静态变量和调用静态方法。

```dart
class MathUtils {
  static const double pi = 3.14159;

  static double calculateArea(double radius) {
    return pi * radius * radius;
  }
}

void main() {
  print(MathUtils.pi);  // 输出 3.14159
  MathUtils.pi = 3.14;

  final area = MathUtils.calculateArea(2);  // 计算半径为2的圆的面积
  print(area);  // 输出 12.56636
}
```

静态方法中是不能直接使用 `普通成员变量/方法` 的。因为普通成员受控于 `对象` ，只有对象才能调用，而在静态方法中是没有当前实例对象的。



# 二、继承

## 1. 继承的概念和用途

在面向对象编程中，继承是一种能够创建新类的方式，我们可以在新类中添加新的方法和字段，也可以对父类的方法进行覆写或扩展。

## 2. 子类和父类

在 Dart 中，我们可以使用 `extends` 关键字来创建一个子类：

```dart
class Animal {
  String name = '';
  
  Animal(this.name);
    
  void eat() {
    print('Eating...');
  }
}

class Cat extends Animal {
  final String type;
  
  Cat(super.name, {required this.type});
  
  void meow() {
    print('Meow...');
  }
}

var cat = Cat();
cat.eat();  // 输出 Eating...
cat.meow();  // 输出 Meow...
```

在这个例子中，`Cat` 类是 `Animal` 类的子类，因此 `Cat` 类的对象可以访问 `Animal` 类的所有公有方法。在 `Cat` 类中可以定义额外的成员属性`type`， 另外 `super.name` 语法是：在入参中为父类中的成员赋值。

## 3. 使用super关键字访问父类

在 Dart 中，我们可以使用 `super` 关键字来访问父类的方法：

```dart
class Animal {
  void eat() {
    print('Eating...');
  }
}

class Cat extends Animal {
  void eat() {
    print('Cat eating...');
    super.eat();
  }
}

var cat = Cat();
cat.eat();  
// 输出：
// Cat eating...
// Eating...
```

在这个例子中，`Cat` 类覆写了 `Animal` 类的 `eat` 方法，并在 `Cat` 类的 `eat` 方法中使用 `super.eat()` 来调用 `Animal` 类的 `eat` 方法。

## 4. 方法覆写

如果子类和父类有同名的方法，那么在子类中的方法会覆写父类中的方法：

```dart
class Animal {
  void eat() {
    print('Eating...');
  }
}

class Cat extends Animal {
  @override
  void eat() {
    print('Cat eating...');
  }
}

var cat = Cat();
cat.eat();  // 输出 Cat eating...
```

**使用@override注解**,在 Dart 中，我们可以使用 `@override` 注解来表示子类的方法覆写了父类的方法。这是一种良好的编程习惯，可以提高代码的可读性。



# 三、多态

多态是面向对象编程的三大特性之一（封装、继承和多态）。在 Dart 中，多态表现为父类引用指向子类对象。这样，父类的引用就可以根据当前指向的子类对象，动态地调用其相应的方法，这是面向对象非常重要的一个特性。

```dart
abstract class Animal {
  void eat();
}

class Cat extends Animal {
  @override
  void eat() {
    print('Cat eating...');
  }
}

class Dog extends Animal {
  @override
  void eat() {
    print('Dog eating...');
  }
}

void feedAnimal(Animal animal) {
  animal.eat();
}

var cat = Cat();
var dog = Dog();
feedAnimal(cat);  // 输出 Cat eating...
feedAnimal(dog);  // 输出 Dog eating...
```

在上述例子中，`feedAnimal` 函数接受一个 `Animal` 类型的参数，然而在运行时，这个参数可以是任何一个 `Animal` 的子类的实例。这就是多态的体现。

## 1. 抽象类

抽象类是一种特殊的类，它不能被实例化。抽象类用于定义一些基本的结构，而具体的实现则由继承抽象类的子类来完成。

抽象类使用 `abstract` 关键字来定义。

```dart
abstract class Animal {
  void eat();  // 抽象方法
}

class Cat extends Animal {
  @override
  void eat() {
    print('Cat eating...');
  }
}
```

在上述例子中，`Animal` 是一个抽象类，它定义了一个抽象方法 `eat`。`Cat` 类继承了 `Animal` 类，并提供了 `eat` 方法的具体实现。

## 2. 接口

Dart 中没有专门的接口关键字，类可以作为接口被其他类实现。实现接口需要使用 `implements` 关键字。

```dart
class Animal {
  void eat() {
    print('Eating...');
  }
}

class Cat implements Animal {
  @override
  void eat() {
    print('Cat eating...');
  }
}
```

在上述例子中，`Animal` 类作为接口被 `Cat` 类实现。`Cat` 类需要提供 `Animal` 中所有方法的实现。

## 3. 多态的限制

多态在 `屏蔽派生类对象之间差异性` 的同时，也会 `屏蔽掉派生类各自的特点`。在 `tag1` 处，将 `Rectangle` 对象声明为 `Shape` 对象，那么你就无法访问到矩形的宽高。同样在 `drawShape` 中，入参是 `Shape` 对象，在方法体中就无法访问派生类中定义的额外成员。

```dart
Shape rectangle = Rectangle(Vec2(10,10)); //tag1
// rectangle.width // Error, 无法访问！

void drawShape(Shape shape){
    shape.draw();
}
```

如果实在想通过基类对象访问派生类的成员，也有途径，可以通过 `is` 关键字来校验是否是 `Rectangle` ，在执行相关代码：

```dart
void drawShape(Shape shape){
    shape.draw();
    if(shape is Rectangle){
      print("绘制矩形: 宽高(${shape.width},${shape.height})");
    }
}
```

## 4. 抽象类与工厂构造

有些抽象类似乎可以调用构造方法进行实例化。`Exception` 是抽象类：

```dart
void main(){
  Exception exception = Exception("hello");
}
```

其实这只是个语法糖，对于抽象类来说，可以通过 `factory` 关键字定义 `工厂构造方法` 。在方法体中返回的依然是 `派生类` 对象。比如下面 `Exception` 工厂构造中返回的是 `_Exception` 对象。

可以通过 `runtimeType` 来查看对象的运行时类型，抽象类不允许被 `直接` 实例化。但可以借助工厂构造来实例化派生类对象。

```dart
void main(){
  Exception exception = Exception("hello");
  print(exception.runtimeType); // _Exception
}
```







# 四、更多特性

除了前面介绍的类、对象、继承、多态、抽象类和接口之外，Dart语言还提供了一些其他的面向对象的特性。这些特性可以帮助开发者更好地组织和设计他们的代码，增加代码的灵活性和可复用性。本文将深入探讨Dart中的工厂构造函数、静态成员和Mixins这些特性。

## 1. 工厂构造函数

Dart中的工厂构造函数（Factory Constructor）是一种特殊类型的构造函数，它可以返回对象的实例，而不一定是类的实例。工厂构造函数通常用于创建复杂对象或在创建对象时执行额外的逻辑。

在类中定义工厂构造函数需要使用`factory`关键字，并且必须返回一个对象。

```dart
class Logger {
  final String name;

  static final Map<String, Logger> _cache = {};

  factory Logger(String name) {
    if (_cache.containsKey(name)) {
      return _cache[name]!;
    } else {
      final logger = Logger._internal(name);
      _cache[name] = logger;
      return logger;
    }
  }

  Logger._internal(this.name);

  void log(String message) {
    print('$name: $message');
  }
}

void main() {
  final logger1 = Logger('Logger');
  final logger2 = Logger('Logger');

  print(identical(logger1, logger2));  // 输出 true，表示logger1和logger2是同一个对象
}
```

在上面的示例中，`Logger`类中定义了一个工厂构造函数`factory Logger(String name)`，用于创建`Logger`对象。通过使用工厂构造函数和静态成员变量`_cache`，我们可以确保相同名称的`Logger`对象只被创建一次。

## 2. 混入 Mixins

Mixins 是一种在 Dart 中实现代码重用和组合的方式。通过使用 mixins，我们可以将一个或多个类的功能合并到一个类中，以便可以复用这些功能，而无需继承类。

### 2.1. mixins 使用

使用`with`关键字将 mixins 应用到其他类中。一个类可以混入若干个类，通过 `,` 号隔开。

```dart
class CanFly {
  void fly() {
    print('Flying...');
  }
}

class CanSwim {
  void swim() {
    print('Swimming...');
  }
}

class Duck with CanFly, CanSwim {
  void quack() {
    print('Quack!');
  }
}

void main() {
  final duck = Duck();
  duck.fly();  // 输出 Flying...
  duck.swim();  // 输出 Swimming...
  duck.quack();  // 输出 Quack!
}
```

在上述示例中，我们定义了两个 mixins：`CanFly` 和 `CanSwim`，它们分别具有 `fly()` 和 `swim()` 方法。然后，我们创建了一个名为 `Duck` 的类，并将 mixins 应用到 `Duck` 类中。通过使用 mixins，`Duck` 类获得了 `CanFly` 和 `CanSwim` 类中的功能，并实现了自己的方法 `quack()`。

值得注意一点的是：混入类支持 `抽象方法` ，而且同样要求派生类必须实现 `抽象方法` 。

```dart
mixin PaintAble{
  late Paint painter;
  void paint(){
    print("=====$runtimeType paint====");
  }
  void init();// tag1
}

class Shape with MoveAble,PaintAble{
  @override
  void init() {
    painter = Paint();
  }
}
```

### 2.2. 定义 minixs

混入类通过 `mixin` 关键字进行声明，其中可以持有 `成员变量` ，也可以声明和实现成员方法。

```dart
void main(){
  Shape shape = Shape();
  shape.speed = 20; 
  shape.move();//=====Shape move====
  print(shape is MoveAble);// true
}

mixin MoveAble{
  double speed = 10;
  void move(){
    print("=====$runtimeType move====");
  }
}

class Shape with MoveAble{}
```

混入类不能拥有【构造方法】，因此`混入类` 无法直接创建对象。

对于多混入来说，混入类的顺序是至关重要的，当存在二义性问题时，会 `“后来居上”` ，访问最后混入类的方法或变量。

另外，混入类并非仅由`mixin` 声明，一切满足 `没有构造方法` 的类都可以作为混入类。

### 2.3. 混入类间的继承

两个混入类间可以通过 `on` 关键字产生类似于 `继承` 的关系：如下 `MoveAble on Position` 之后，`MoveAble` 类中可以访问 `Position` 中定义的 `vec2` 成员变量。

`on` 关键字，并不是用来表示继承的关系，而是用来限定可以使用该 mixin 的类型。比如 `mixin A on B` 代表 A 只能在 B 及其衍生类中被混入。

```dart
void main(){
  Shape shape = Shape();
  shape.speed = 20;
  shape.move();//=====Shape move====
  print(shape is MoveAble);// true
}

mixin Position{
  Vec2 vec2 = Vec2(0, 0);
}

mixin MoveAble on Position{
  double speed = 10;
  void move(){
    vec2.x+=speed;
    vec2.y+=speed;
    print("=====$runtimeType move====");
  }
}

mixin PaintAble{
  double speed = 10;
  void paint(){
    print("=====$runtimeType paint====");
  }
}

class Shape with Position,MoveAble,PaintAble{}

class Vec2{
  double x;
  double y;
  Vec2(this.x, this.y);
}
```

注意，由于 `MoveAble on Position` ，当 `Shape with MoveAble` 时，必须在 `MoveAble` 之前混入 `Position` 。

## 3. Dart 中接口

`Dart` 中并不像 `Java` 那样，有明确的关键字作为 `接口类` 的标识。因为 `Dart` 中的接口概念不再是 `传统意义` 上的狭义接口。而是 `Dart` 中的任何类都可以作为接口，包括普通的类。

- 当 `C` 类实现 `A` 、`B` 接口，必须强制覆写 `所有` 成员方法
- 当 `C` 类实现 `A` 、`B` 接口，必须强制覆为 `所有` 成员变量提供 `get` 方法

```dart
class A{
  final String name;
  A(this.name);
 
  void run(){
    print("run in a");
  }
}

class B{
  final String name;
  B(this.name);

  void run(){
    print("run in a");
  }

  void log(){
    print("log in a");
  }
}

class C implements A, B {
  @override
  String get name => "C";

  @override
  void log() {}

  @override
  void run() {}
}
```

对于继承来说，派生类只需要实现抽象方法即可，`抽象基类` 中的普通成员方法可以不覆写。`implements` 关键字要求派生类必须覆写 `接口` 中的 `所有 `方法 。

## 4. 类的运算符重载

对象间通过运算符的操作，在某些场景下可以大大提高可读性和简洁性。

比如现在想让两个 `Vec2` 相加，获得一个新的 `Vec2` 对象。

```dart
class Vec2 {
  final double x;
  final double y;
  Vec2(this.x, this.y);

  Vec2 add(Vec2 other) => Vec2(other.x + x, other.y + y);
}

void main() {
  Vec2 p0 = Vec2(3, 4);
  Vec2 p1 = Vec2(2, 5);
  Vec2 p2 = p0.add(p1);
  Vec2 p3 = p0.add(p1).add(p0).add(p2);
  print(p2); //Vec2(5.0,9.0)
}
```

 `运算符重载`：使用 `operator` 关键字加上 `运算符` 作为方法名，加法是二元运算符，所以方法中有一个入参。该入参类型就是使用时 `+` 后面的对象类型：

```dart
class Vec2 {
  final double x;
  final double y;
  Vec2(this.x, this.y);
  
  Vec2 operator +(Vec2 other) => Vec2(other.x + x, other.y + y);
}

Vec2 p2 = p0 + p1 + p0 + p1; 
```

虽然运算符重载在某些场景下可以增强语义，但如果乱用，反而可能会产生一些不明所以的语句。比如下面拓展了 `[]` 运算符，传入 `bool` 值，如果为 `true` 返回 `x` ；反之返回 `y` 。

```dart
class Vec2 {
  final double x;
  final double y;
  Vec2(this.x, this.y);

  double operator [](bool flag) => flag ? x : y;
}

Vec2 p0 = Vec2(3, 4);
double x = p0[true];
print(x); // 3.0
```

通过 `p0[true]` 可以获取 `x` 值，但在别人眼里这种语句就会显得莫名其妙，应尽量避免写出这种花里胡哨的代码。

## 5. 类的拓展方法

`Dart` 在 `2.7` 版本后支持了 `类拓展方法` ，关键字是 `extension` 。该特性支持在某类定义文件之外，拓展该类的方法，在其中可以访问类成员。这对一些三方库或者框架内不便修改的类拓展功能是非常有益的。

如下：为 `String` 拓展 `isPhone` 的方法来校验字符串是不是手机号。语法上来看，使用 `extension A on B` 来定义，其中 `A` 的名字是任意的，`B` 是拓展的目标类。如下 `isPhone` 就相当于 `String` 中的一个成员方法，可以访问 `this` 对象。

```dart
extension JudgeStringExt on String{
  bool isPhone(){
    const String reg = r'^(13[0-9]|14[01456879]|15[0-35-9]|16[2567]|17[0-8]|18[0-9]|19[0-35-9])\d{8}$';
    RegExp(reg).hasMatch(this);
    return RegExp(reg).hasMatch(this);
  }
}

void main() {
  String input = "18715079839";
  bool checked = input.isPhone();
  print(checked); // true
}
```

注意，`运算符` 本身也是一种方法，所以支持拓展。如下是对 `>` 的拓展，用于判断配个 `String` 首位字符的大小。

```dart
bool operator >(String other) {
  int thisCode = 0;
  int otherCode = 0;
  if (isNotEmpty) {
    thisCode = codeUnits.first;
  }
  if (other.isNotEmpty) {
    otherCode = other.codeUnits.first;
  }
  return thisCode > otherCode;
}

// 使用
print("hello" > "toly"); // flase
```

另外注意一点，拓展方法只能拓展 `成员方法` ，不支持拓展 `普通成员变量` ，而且不能在拓展在原类中已存在的方法。当拓展中定义`静态`成员变量、`静态`成员方法时，只归拓展类所属，无法拓展到目标类。

## 6. 对象的几个符号

`??` 符号，它前面是变量，后面是默认值，表示如果前者为 `null`，表达式取默认值。

```dart
void main() {
  foo(null); // UNKNOWN
  foo("toly"); // toly
}

void foo(String? arg) {
  String b = arg ?? "UNKNOWN";
  print(b);
}
```

变量提供 `.` 符号可以访问成员属性和调用成员方法，在使用时 `..` 可以实现连续的调用。

```dart
void main() {
  Person toly = Person();
  toly.name = "toly";
	toly..name = "toly"..age = 28..log();
}

class Person {
  String name = '';
  int age = 0;

  void log(){}
}
```

`...` 用于解构可迭代对象，是一个非常简便的操作

```dart
void main() {
  List<int> list = [0, 1, 2, 3, 4];
  List<int> list2 = [6, ...list, 7];
  print(list2); // [6, 0, 1, 2, 3, 4, 7]
}
```



















