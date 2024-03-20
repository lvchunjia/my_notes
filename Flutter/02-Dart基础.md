

> 版权：本文摘抄自[编程时光 (coding-time.cn)](https://www.coding-time.cn/dart/preamble.html)，仅用个人记录学习

## 一、变量

变量是我们在编程中存储和操控数据的基本单位。在Dart中，我们有多种方式来声明和使用变量。

使用 `var` 来声明一个变量，Dart会自动推断出变量类型。

```dart
var name = 'Dart'; // Dart 自动推断出 `name` 是 String 类型
```

在声明变量时明确指定其类型，这样可以使得代码更易于理解，并且在编译时能够检查到类型错误。

```dart
String greeting = 'Hello Dart'; 
```

Dart2.12版本引入了空安全特性，如果变量可能含有空值，我们需要在类型后面加一个问号`?`。

```dart
String? nullableString = null;
```

如果一个变量在初始化后值不再改变，可以使用 `final` 或 `const` 声明它，这样可以使我们的程序更加安全。

```dart
final pi = 3.14159; 
const gravity = 9.8; 
```

注意，`final` 和 `const` 的区别在于，`final` 的值只能被设定一次，而 `const` 则是一个编译时常量。

## 二、数据类型

*Dart是一个强类型语言，包含了许多常见的数据类型：*

**Numbers**：包括 `int` 和 `double` 两种类型。

```dart
int age = 18;
double score = 93.5;
```

**Strings**：表示文本的数据类型。可以通过单引号或者双引号来创建字符串。

```dart
String hello = 'Hello';
```

**Booleans**：包括 `true` 和 `false` 两种布尔值。

```dart
bool isTrue = true;
bool isFalse = false;
```

**Lists**：一个有序的项目集合，也被称为数组。

```dart
List<int> numbers = [1, 2, 3];
```

**Maps**：无序的键值对集合。

```dart
Map<String, String> countries = {
  'CN': 'China',
  'US': 'United States',
  'JP': 'Japan'
};
```



## 三、运算符

*运算符是一种特殊的符号，用于检查，更改或结合值。Dart语言中的运算符主要包括以下几类：*

### 1. 算术运算符

算术运算符用于进行数学运算。Dart中的算术运算符有 `+`（加），`-`（减），`*`（乘），`/`（除），`%`（取余）以及`~/`（取整）。

```dart
var a = 10;
var b = 2;

print(a + b); // 输出：12
print(a - b); // 输出：8
print(a * b); // 输出：20
print(a / b); // 输出：5.0
print(a % b); // 输出：0
print(a ~/ b); // 输出：5
```

### 2. 关系运算符

关系运算符用于比较两个值。Dart中的关系运算符有 `==`（等于），`!=`（不等于），`>`（大于），`<`（小于），`>=`（大于或等于），`<=`（小于或等于）。

```dart
var a = 10;
var b = 2;

print(a == b); // 输出：false
print(a != b); // 输出：true
print(a > b); // 输出：true
print(a < b); // 输出：false
print(a >= b); // 输出：true
print(a <= b); // 输出：false
```

### 3. 逻辑运算符

逻辑运算符主要用于Boolean类型的操作，但也可以用于非Boolean类型。Dart中的逻辑运算符有 `&&`（逻辑与），`||`（逻辑或），`!`（逻辑非）。

```dart
var a = true;
var b = false;

print(a && b); // 输出：false
print(a || b); // 输出：true
print(!a); // 输出：false
```

###  4. 赋值运算符

赋值运算符用于给变量赋值。Dart中的赋值运算符有 `=`，`+=`，`-=`，`*=`，`/=`，`%=`，`~/=`。

```dart
var a = 10;
var b = 2;

a = b;
print(a); // 输出：2

a += b;
print(a); // 输出：4

a -= b;
print(a); // 输出：2

a *= b;
print(a); // 输出：4

a ~/= b;
print(a); // 输出：2

a %= b;
print(a); // 输出：0
```

### 5. 条件运算符

Dart提供了两种类型的条件运算符，分别是 `? :` 和 `??`。其中 `? :` 可以在基于条件的情况下返回两个值中

的一个，`??` 用于在第一个操作数为null时返回第二个操作数。

```dart
var a = 10;
var b = null;

print(a > 10 ? 'a is greater than 10' : 'a is not greater than 10'); // 输出：a is not greater than 10
print(b ?? 'default value'); // 输出：default value
```

### 6. 类型测试运算符

类型测试运算符用于检查对象的类型。Dart中的类型测试运算符有 `is` 和 `is!`。

```dart
var a = 10;

print(a is int); // 输出：true
print(a is! String); // 输出：true
```

### 7. 位运算符

位运算符用于对整数进行二进制位运算。Dart中的位运算符有 `&`（与），`|`（或），`^`（异或），`~`（非），`>>`（右移），`<<`（左移）。

```dart
var a = 10; // 二进制形式：1010
var b = 2; // 二进制形式：0010

print(a & b); // 输出：2
print(a | b); // 输出：10
print(a ^ b); // 输出：8
print(~a); // 输出：-11
print(a >> b); // 输出：2
print(a << b); // 输出：40
```

### 速查表

以下列出了 Dart 的运算符，从高到低按照优先级排列：

| 描述               | 运算符                                     |
| ------------------ | ------------------------------------------ |
| 一元运算符（后置） | ++ -- ( ) [ ] . ?.                         |
| 一元运算符（前置） | - ! ~ ++ --                                |
| 乘法运算符         | * / % ~/                                   |
| 加法运算符         | + -                                        |
| 移位运算符         | << >>                                      |
| 按位与             | &                                          |
| 按位异或           | ^                                          |
| 按位或             | \|                                         |
| 关系与类型检测     | >= > <= < as is is!                        |
| 逻辑与             | &&                                         |
| 逻辑或             | \|\|                                       |
| 是否为null         | ??                                         |
| 条件运算符         | ? :                                        |
| 级联运算符         | ..                                         |
| 赋值运算符         | = *= /= ~/= %= += -= <<= >>= &= ^= \|= ??= |



| 运算符 | 介绍                                                         | 示例                                                         |
| ------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| ?.     | 点符号前加问号，表示当前调用只在被访问者不为null的情况下才执行 | `var upper = name?.toUpperCase();`                           |
| is is! | 检查对象是否属于或不属于某种类型                             | `if (name is String) { ... }`                                |
| as     | 将对象转换为某类型，如果转换失败将抛出异常                   | `name as String`                                             |
| ??     | 空值检测，如：a1 ?? a2 ，表示如果a1不为null，则直接返回a1的值，否则返回a2的值 | `var message = input ?? 'Hello';`                            |
| ..     | 级联操作符，用于对同一对象执行一系列操作（链式操作），避免创建多余的临时变量 | 不使用级联：`person.name = 'bob'; person.age = 28;` 使用级联：`person..name = 'bob' ..age = 28;` |
| ??=    | 空值判断赋值，只在左值为null的情况下才执行赋值操作           | `message ??= 'Hello';`                                       |

## 四、流程控制

*Dart语言提供了一套丰富的控制流语句，包括各种条件语句和循环语句，让你可以实现各种复杂的逻辑。*

### 1. 条件语句

Dart中的条件语句主要有`if`和`else`。使用`if`和`else`可以根据特定的条件执行特定的代码。

```dart
var num = 10;

if (num > 5) {
  print('Number is greater than 5');
} else {
  print('Number is equal to or less than 5');
}
```

另外，Dart还支持`else if`语句，用于检查多个条件。

```dart
var num = 10;

if (num > 10) {
  print('Number is greater than 10');
} else if (num == 10) {
  print('Number is equal to 10');
} else {
  print('Number is less than 10');
}
```

### 2. 循环语句

*在Dart中，你可以使用`for`循环，`while`循环，和`do-while`循环。*

- `for`循环

`for`循环是最常用的循环类型，它可以指定循环次数。

```dart
for (var i = 0; i < 5; i++) {
  print('Hello Dart $i');
}
```

- `while`循环

`while`循环会在条件满足时持续循环。

```dart
var num = 5;
while (num > 0) {
  print('Hello Dart $num');
  num--;
}
```

- `do-while`循环

`do-while`循环与`while`循环类似，区别在于`do-while`循环会先执行一次循环体，然后再检查条件。

```dart
var num = 5;
do {
  print('Hello Dart $num');
  num--;
} while (num > 0);
```

### 3. `break`和`continue`

在循环中，`break`语句可以用来立即终止循环，而`continue`语句可以用来跳过当前循环中剩余的代码，直接开始下一次循环。

```dart
for (var i = 0; i < 10; i++) {
  if (i == 5) {
    break;
  }
  print('Hello Dart $i');
}

for (var i = 0; i < 10; i++) {
  if (i == 5) {
    continue;
  }
  print('Hello Dart $i');
}
```

### 4. `switch`和`case`

`switch`和`case`语句用于基于不同的情况执行不同的代码。

```dart
var grade = 'A';

switch (grade) {
  case 'A':
    print('Excellent');
    break;
  case 'B':
    print('Good');
    break;
  case 'C':
    print('Fair');
    break;
  case 'D':
    print('Poor');
    break;
  default:
    print('Invalid grade');
}
```

注意：在每个`case`子句后面都需要有一个`break`语句，否则会发生错误。`default`子句是可选的，用于处理所有未被其他`case`子句处理的情况。

## 五、函数

*Dart语言作为一门面向对象的语言，函数在其中占据了非常重要的位置。本文将详细解析如何定义和调用函数，以及箭头语法，高阶函数和闭包等内容。*

### 1. 函数的定义和调用

在Dart中，函数可以定义为一段实现特定功能的代码块，可以带有参数和返回值。

定义函数：

```dart
void printHello(String name) {
  print('Hello, $name');
}
```

调用函数：

```dart
printHello('Dart');
```

### 2. 箭头语法

当函数体只有一句话的时候，我们可以使用箭头语法来简化函数的定义。

```dart
void printHello(String name) => print('Hello, $name');

printHello('Dart');
```

### 3. 高阶函数

高阶函数是指可以接收函数作为参数，或者返回函数的函数。Dart语言支持高阶函数。

例如，下面的`calculate`函数接受两个参数和一个函数，然后使用传入的函数来操作参数：

```dart
void calculate(int a, int b, Function operation) {
  print(operation(a, b));
}

calculate(2, 3, (a, b) => a * b);
```

### 4. 闭包

在Dart中，闭包可以定义为一个函数对象，即使其函数对象的调用在它原始范围之外，也能够访问在它词法范围内的变量。换句话说，闭包是一个能够读取其他函数内部变量的函数。

```dart
Function makeAdder(int addBy) {
  return (int i) => addBy + i;
}

void main() {
  var adder = makeAdder(2);
  print(adder(3)); // 输出5
}
```

在上述代码中，`makeAdder`函数返回一个新的函数，这个新的函数能够访问`makeAdder`函数的内部变量`addBy`。

## 六、Dart中的集合类型

*Dart 提供了一系列的集合类型，其中包括 Map 和 Set。本文将简要介绍 Dart 中的 Map 和 Set，以及如何在 Dart 中使用这两种数据结构。*

### 1.Dart中的List

Dart中的List是一种重要的数据类型，可以存储一系列有序的元素，元素的类型可以是任意类型，包括数字，字符串，布尔值，对象，甚至是其他List。它类似于其他编程语言中的数组，但具有更多的内置方法和功能。

#### 创建和初始化List

在Dart中，你可以通过几种不同的方式创建和初始化List：

```dart
// 创建空列表
var emptyList = [];
// 创建具有几个初始元素的列表
var initializedList = [1, 2, 3, 4, 5];
// 使用List构造函数创建列表
var listWithConstructor = List<int>.filled(5, 0); // 创建一个包含5个0的列表
```

#### 访问和修改List元素

你可以使用索引（从0开始）来访问和修改List中的元素：

```dart
var myList = [1, 2, 3];
print(myList[0]);  // 输出1
myList[0] = 10;
print(myList[0]);  // 输出10
```

#### List的主要方法

List类提供了一些方法来处理和操作列表。

- `add(element)`: 在List的末尾添加一个元素
- `insert(index, element)`: 在指定索引处插入一个元素
- `remove(element)`: 删除列表中首个匹配的元素
- `removeAt(index)`: 删除指定索引处的元素
- `indexOf(element)`: 查找指定元素的索引，如果元素不存在，则返回-1
- `contains(element)`: 检查列表是否包含指定元素，如果包含则返回true，否则返回false
- `sort([compareFunction])`: 对List的元素进行排序，可以提供一个可选的比较函数

```dart
var myList = [1, 2, 3];

myList.add(4);
print(myList);  // 输出 [1, 2, 3, 4]

myList.insert(0, 0);
print(myList);  // 输出 [0, 1, 2, 3, 4]

myList.remove(2);
print(myList);  // 输出 [0, 1, 3, 4]

myList.removeAt(0);
print(myList);  // 输出 [1, 3, 4]

print(myList.indexOf(3));  // 输出 1

print(myList.contains(2));  // 输出 false

myList.sort();
print(myList);  // 输出 [1, 3, 4]
```

### 2.Dart中的Map

Dart中的Map是一种无序的键值对集合，其中的键和值都可以是任何类型。它是一个动态集合，这意味着你可以在运行时向其中添加或删除键值对。Map在很多场景下都很有用，例如，当你需要通过一种方式（键）来查找或访问数据（值）时。

#### 创建和初始化Map

在Dart中，你可以通过以下几种方式创建和初始化Map：

```dart
// 创建空的Map
var emptyMap = {};

// 创建并初始化Map
var initializedMap = {
  'key1': 'value1',
  'key2': 'value2',
  'key3': 'value3',
};

// 使用Map构造函数创建Map
var mapWithConstructor = Map();
```

#### 访问和修改Map元素

你可以通过键来访问和修改Map中的值：

```dart
var myMap = {
  'key1': 'value1',
  'key2': 'value2',
};

print(myMap['key1']);  // 输出 'value1'

myMap['key1'] = 'new value1';
print(myMap['key1']);  // 输出 'new value1'
```

#### Map的主要方法

Map类提供了一些方法来处理和操作键值对。

- `containsKey(key)`: 检查Map是否包含指定的键
- `containsValue(value)`: 检查Map是否包含指定的值
- `remove(key)`: 删除指定的键及其对应的值
- `addAll(other)`: 将其他Map的键值对添加到当前Map中
- `clear()`: 删除Map中的所有键值对

```dart
var myMap = {
  'key1': 'value1',
  'key2': 'value2',
};

print(myMap.containsKey('key1'));  // 输出 true
print(myMap.containsValue('value3'));  // 输出 false

myMap.remove('key1');
print(myMap);  // 输出 {key2: value2}

myMap.addAll({'key3': 'value3', 'key4': 'value4'});
print(myMap);  // 输出 {key2: value2, key3: value3, key4: value4}

myMap.clear();
print(myMap);  // 输出 {}
```

### 3.Dart中的Set

Dart中的Set是一种无序的、包含唯一项的集合，所有的元素都是唯一的，没有重复项。这意味着无论你尝试将同样的项目添加到Set中多少次，它都只会出现一次。

#### 创建和初始化Set

在Dart中，你可以通过以下几种方式创建和初始化Set：

```dart
// 创建空的Set
var emptySet = <String>{};
// 创建并初始化Set
var initializedSet = {'item1', 'item2', 'item3'};

// 使用Set构造函数创建Set
var setWithConstructor = Set<String>();
```

注意：如果你尝试创建一个空的Set但未指定类型，Dart会创建一个动态类型的Map。因此，为了创建一个空的Set，你需要在创建Set时提供一个类型参数。

#### 添加和删除Set元素

你可以使用`add`和`remove`方法向Set中添加或删除元素：

```dart
var mySet = {'item1', 'item2', 'item3'};

mySet.add('item4');
print(mySet);  // 输出 {item1, item2, item3, item4}

mySet.remove('item1');
print(mySet);  // 输出 {item2, item3, item4}
```

#### Set的主要方法

Set类提供了一些方法来处理和操作集合。

- `contains(element)`: 检查Set是否包含指定的元素
- `union(other)`: 返回一个新的Set，包含当前Set和另一个Set中所有的元素
- `intersection(other)`: 返回一个新的Set，包含当前Set和另一个Set中共有的元素
- `difference(other)`: 返回一个新的Set，包含当前Set中的元素，但不包含另一个Set中的元素

```dart
var mySet1 = {'item1', 'item2', 'item3'};
var mySet2 = {'item2', 'item3', 'item4'};

print(mySet1.contains('item1'));  // 输出 true

var unionSet = mySet1.union(mySet2);
print(unionSet);  // 输出 {item1, item2, item3, item4}

var intersectionSet = mySet1.intersection(mySet2);
print(intersectionSet);  // 输出 {item2, item3}

var differenceSet = mySet1.difference(mySet2);
print(differenceSet);  // 输出 {item1}
```













