



# 一、类和对象

面向对象编程（Object Oriented Programming，简称OOP）是一种编程范型，它使用 "对象"：包含数据字段（属性）和在对象上执行操作的方法。这是一种设计和结构化代码的方式，允许我们创建复杂的应用程序，使用基本代码构建并易于理解和维护。

Dart 作为一种面向对象的类定义语言，使用混合的继承模式：即，Dart 中的类只能有一个超类，但可以实现多个接口。类定义的语法非常接近于 C-style 的语言（如 Java、C++ 和 JavaScript），这使得大多数开发者可以快速理解和学习 Dart。

## 1.类的定义

在 Dart 中，我们可以通过 `class` 关键字来定义一个类。类是一种复合的数据类型，即它包含方法（函数）和变量（称为"属性"）。

```dart
class Person {
  String name;
  int age;

  void sayHello() {
    print('Hello, my name is $name, I am $age years old.');
  }
}
```

在这个例子中，我们定义了一个名为 `Person` 的类，它有两个属性 `name` 和 `age`，还有一个方法 `sayHello`。

## 2.创建对象

创建类的实例（也就是对象），我们可以使用 `new` 关键字，然后调用类的构造函数。在 Dart 2 中，`new` 关键字是可选的：

```dart
var person = Person();
person.name = 'Alice';
person.age = 20;
person.sayHello();
```

## 3.访问属性和方法

我们可以使用 `.` 符号来访问对象的属性和方法：

```dart
print(person.name);  // 输出 Alice
person.sayHello();  // 输出 Hello, my name is Alice, I am 20 years old.
```

## 4.构造函数

在 Dart 中，构造函数的名称与类的名称相同，我们可以在构造函数中初始化对象的属性：

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

## 5.this关键字的使用

在 Dart 中，`this` 关键字引用的是当前实例。我们可以在构造函数或其他方法中使用 `this` 关键字来访问当前对象的属性或方法。

## 6.getter和setter方法

在 Dart 中，我们可以使用 getter 和 setter 方法来读取和写入对象的属性：

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

## 7.私有属性和方法

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

在上面的代码中，`_name`、`_age` 和 `_privateMethod` 都是私有的，只能在 `Person` 类内部访问。



# 二、继承

## 1.继承的概念和用途

在面向对象编程中，继承是一种能够创建新类的方式，我们可以在新类中添加新的方法和字段，也可以对父类的方法进行覆写或扩展。

## 2.子类和父类

在 Dart 中，我们可以使用 `extends` 关键字来创建一个子类：

```dart
class Animal {
  void eat() {
    print('Eating...');
  }
}

class Cat extends Animal {
  void meow() {
    print('Meow...');
  }
}

var cat = Cat();
cat.eat();  // 输出 Eating...
cat.meow();  // 输出 Meow...
```

在这个例子中，`Cat` 类是 `Animal` 类的子类，因此 `Cat` 类的对象可以访问 `Animal` 类的所有公有方法。

## 3.使用super关键字访问父类

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

## 4.方法覆写

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

## 1.抽象类

在 Dart 中，抽象类是一种特殊的类，它不能被实例化。抽象类用于定义一些基本的结构，而具体的实现则由继承抽象类的子类来完成。抽象类使用 `abstract` 关键字来定义。

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

## 2.接口

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

这样我们就初步介绍了 Dart 中面向对象编程的主要概念和用法。实际上，Dart 中面向对象的特性还有很多，例如工厂构造函数、静态成员、Mixins 等。这些内容需要我们在日常的学习和实践中不断深入理解和掌握。



# 四、更多特性

除了前面介绍的类、对象、继承、多态、抽象类和接口之外，Dart语言还提供了一些其他的面向对象的特性。这些特性可以帮助开发者更好地组织和设计他们的代码，增加代码的灵活性和可复用性。本文将深入探讨Dart中的工厂构造函数、静态成员和Mixins这些特性。

## 1.工厂构造函数 

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

## 2.静态成员

静态成员是属于类本身而不是类的实例的成员。可以通过在成员前面加上`static`关键字来定义静态成员。静态成员在类的所有实例之间共享，并且可以通过类名直接访问，无需创建类的实例。

静态成员包括静态变量和静态方法。以下是一个示例：

```dart
class MathUtils {
  static const double pi = 3.14159;

  static double calculateArea(double radius) {
    return pi * radius * radius;
  }
}

void main() {
  print(MathUtils.pi);  // 输出 3.14159

  final area = MathUtils.calculateArea(2);  // 计算半径为2的圆的面积
  print(area);  // 输出 12.56636
}
```

在上述示例中，`MathUtils`类中定义了一个静态变量`pi`和一个静态方法`calculateArea`。我们可以直接通过类名访问静态变量和调用静态方法。

## 3.Mixins

Mixins 是一种在 Dart 中实现代码重用和组合的方式。通过使用 mixins，我们可以将一个或多个类的功能合并到一个类中，以便可以复用这些功能，而无需继承类。

要使用 mixins，需要定义一个特殊的类，并使用`with`关键字将 mixins 应用到其他类中。

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











