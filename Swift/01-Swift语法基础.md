> 

## 一、基础

### 1. 变量 let、var

变量是可变的，使用 var 修饰，常量是不可变的，使用 let 修饰。类、结构体和枚举里的变量是属性。

```swift
var v1:String = "hi" // 标注类型
var v2 = "类型推导"
let l1 = "标题" // 常量

class a {
    let p1 = 3
    var p2: Int {
        p1 * 3
    }
}
```

属性没有 set 可以省略 get，如果有 set 需加 get。变量设置前通过 willSet 访问到，变量设置后通过 didSet 访问。

### 2. 注释

```swift
// 单行注释
/*
多行注释第一行。
多行注释第二行。
*/ 
// MARK: 会在 minimap 上展示
// TODO: 待做
// FIXME: 待修复
```

控制台打印值

```swift
print("hi")
let i = 14
print(i)
print("9月\(i)是小柠檬的生日")

for i in 1...3{
    print(i)
}
// output:
// 1
// 2
// 3

// 使用terminator使循环打印更整洁
for i in 1...3 {
    print("\(i) ", terminator: "")
}
// output:
// 1 2 3
```



### 3. 可选变量`?`

- 使用`?`声明可选变量，可能会是 `nil` 的变量就是可选变量。

- 当变量为 `nil`， 通过 `??` 操作符可以提供一个默认值。

- 可选类型不支持类型推断
- 使用`!`声明隐式解包可选变量

```swift
// 基本使用
var o: Int? = nil
let i = o ?? 0 // 默认值

// 解包
let s1: String? = "hey"
let s2: String? = "u"

// 方式一
if let s0 = s1 {
    print(s1)
}
// 方式二
print(s2!)

guard let s1, let s2 else { return }
print(s1 + " " + s2)
```



## 二、数据类型

### 1. 字符串

```swift
let s1 = "Hi! This is a string. Cool?"

/// 转义符 \n 表示换行。
/// 其它转义字符有 \0 空字符)、\t 水平制表符 、\n 换行符、\r 回车符
let s2 = "Hi!\nThis is a string. Cool?"

// 多行
let s3 = """
Hi!
This is a string.
Cool?
"""

// 长度
print(s3.count)
print(s3.isEmpty)

// 拼接
print(s3 + "\nSure!")

// 字符串中插入变量
let i = 1
print("Today is good day, double \(i)\(i)!")

/// 遍历字符串
/// 输出：
/// o
/// n
/// e
for c in "one" {
    print(c)
}

// 查找
print(s3.lowercased().contains("cool")) // true

// 替换
let s4 = "one is two"
let newS4 = s4.replacingOccurrences(of: "two", with: "one")
print(newS4)

// 删除空格和换行
let s5 = " Simple line. \n\n  "
print(s5.trimmingCharacters(in: .whitespacesAndNewlines))

// 切割成数组
let s6 = "one/two/three"
let a1 = s6.components(separatedBy: "/") // 继承自 NSString 的接口
print(a1) // ["one", "two", "three"]

let a2 = s6.split(separator: "/")
print(a2) // ["one", "two", "three"] 属于切片，性能较 components 更好

// 判断是否是某种类型
let c1: Character = "🤔"
print(c1.isASCII) // false
print(c1.isSymbol) // true
print(c1.isLetter) // false
print(c1.isNumber) // false
print(c1.isUppercase) // false

// 字符串和 Data 互转
let data = Data("hi".utf8)
let s7 = String(decoding: data, as: UTF8.self)
print(s7) // hi

// 字符串可以当作集合来用。
let revered = s7.reversed()
print(String(revered))
```

Unicode、Character 和 SubString 等内容参见官方字符串文档：[Strings and Characters — The Swift Programming Language (Swift 5.1)](https://docs.swift.org/swift-book/LanguageGuide/StringsAndCharacters.html)

字符串字面符号可以参看《[String literals in Swift](https://www.swiftbysundell.com/articles/string-literals-in-swift/)》。

原始字符串

```swift
// 原始字符串在字符串前加上一个或多个#符号。里面的双引号和转义符号将不再起作用了，如果想让转义符起作用，需要在转义符后面加上#符号。
let s8 = #"\(s7)\#(s7) "one" and "two"\n. \#nThe second line."#
print(s8)
/// \(s7)hi "one" and "two"\n.
/// The second line.

// 原始字符串在正则使用效果更佳，反斜杠更少了。
let s9 = "\\\\[A-Z]+[A-Za-z]+\\.[a-z]+"
let s10 = #"\\[A-Z]+[A-Za-z]+\.[a-z]+"#
print(s9) // \\[A-Z]+[A-Za-z]+\.[a-z]+
print(s10) // \\[A-Z]+[A-Za-z]+\.[a-z]+
```

### 2. 数字

数字的类型有 Int、Float 和 Double

```swift
// Int
let i1 = 100
let i2 = 22
print(i1 / i2) // 向下取整得 4

// Float
let f1: Float = 100.0
let f2: Float = 22.0
print(f1 / f2) // 4.5454545

let f3: Float16 = 5.0 // macOS 还不能用
let f4: Float32 = 5.0
let f5: Float64 = 5.0
let f6: Float80 = 5.0
print(f4, f5, f6) // 5.0 5.0 5.0

// Double
let d1: Double = 100.0
let d2: Double = 22.0
print(d1 / d2) // 4.545454545454546

// 字面量
print(Int(0b10101)) // 0b 开头是二进制 
print(Int(0x00afff)) // 0x 开头是十六进制
print(2.5e4) // 2.5x10^4 十进制用 e
print(0xAp2) // 10*2^2  十六进制用 p
print(2_000_000) // 2000000

// isMultiple(of:) 方法检查一个数字是否是另一个数字的倍数
let i3 = 36
print(i3.isMultiple(of: 9)) // true
```

处理数字有 floor、ceil、round。floor 是向下取整，只取整数部分；cell 是向上取整，只要有不为零的小数，整数就加1;round 是四舍五入。

### 3. 布尔

布尔数有 true 和 false 两种值，还有一个能够切换这两个值的 toggle 方法。

```swift
var b = false
b.toggle() // true
b.toggle() // false
```

### 4. 元组

元组里的值类型可以是不同的。元组可以看成是匿名的结构体。元组的类型不允许更改。

```swift
let t1 = (p1: 1, p2: "two", p3: [1,2,3])
print(t1.p1)
print(t1.p3)

// 类型推导
let student: (String, Int) = ("rose", 90)
let t2 = (1, "two", [1,2,3])

// 通过下标访问
print(t2.1) // two

// 分解元组
let (dp1, dp2, _) = t2
print(dp1)
print(dp2)
```



### 5. range

- 表示一系列值的数据类型
- 可以是闭区间或者半开区间

```swift
var rangeExample = 1...5
var count = 5
var halfRangeExample = 1..<count
```



## 三、函数式







## 四、操作符

### 1. 赋值

```swift
let i1 = 1
var i2 = i1
i2 = 2
print(i2) // 2

i2 += 1
print(i2) // 3

i2 -= 2
print(i2) // 1

i2 *= 10
print(i2) // 10

i2 /= 2
print(i2) // 5
```

### 2. 计算

```swift
let i1 = 1
let i2 = i1
print((i1 + i2 - 1) * 10 / 2 % 3) // 2
print("i" + "1") // i1

// 一元运算符
print(-i1) // -1
```

### 3. 比较

遵循 Equatable 协议可以使用 == 和 != 来判断是否相等

```swift
print(1 > 2) // false

struct S: Equatable {
    var p1: String
    var p2: Int
}
let s1 = S(p1: "one", p2: 1)
let s2 = S(p1: "two", p2: 2)
let s3 = S(p1: "one", p2: 2)
let s4 = S(p1: "one", p2: 1)

print(s1 == s2) // false
print(s1 == s3) // false
print(s1 == s4) // true
```

类需要实现 == 函数

```swift
class C: Equatable {
    var p1: String
    var p2: Int
    init(p1: String, p2: Int) {
        self.p1 = p1
        self.p2 = p2
    }
    
    static func == (l: C, r: C) -> Bool {
        return l.p1 == r.p1 && l.p2 == r.p2
    }
}

let c1 = C(p1: "one", p2: 1)
let c2 = C(p1: "one", p2: 1)
print(c1 == c2)
// 元组比较
// 会先比较第一个数，第一个无法比较才会比较第二个数
// 字符串比较和字母大小还有长度有关。先比较字母大小，在比较长度
("apple", 1) < ("apple", 2) // true
("applf", 1) < ("apple", 2) // false
("appl", 2) < ("apple", 1) // true
("appm", 2) < ("apple", 1) // false

var a = "a" // 95
var A = "A" // 97
if a > A {
    print("a > A") // true
} else {
    print("A > a")
}
```

### 4. 逻辑

```swift
let i1 = -1
let i2 = 2

if i1 != i2 && (i1 < 0 || i2 < 0) {
    print("i1 and i2 not equal, and one of them is negative number.")
}
```

### 5. 其他

- 三元运算符：简化 if else 写法

```swift
// if else
func f1(p: Int) {
    if p > 0 {
        print("positive number")
    } else {
        print("negative number")
    }
}

// 三元
func f2(p: Int) {
    p > 0 ? print("positive number") : print("negative number")
}

f1(p: 1)
f2(p: 1)
```

- Nil-coalescing?? ：简化 if let else 写法

```swift
// if else
func f1(p: Int?) {
    if let i = p {
        print("p have value is \(i)")
    } else {
        print("p is nil, use defalut value")
    }
}

// 使用 ??
func f2(p: Int?) {
    let i = p ?? 0
    print("p is \(i)")
}
```

- 范围a...b：简化的值范围表达方式。

```swift
// 封闭范围
for i in 0...10 {
    print(i)
}

// 半开范围
for i in 0..<10 {
    print(i)
}
// 单侧区间
let nums = [5,6,7,8]
print(nums[2...]) // 7 8
```

- 恒等 ===, !==：恒等返回是否引用了相同实例。

```swift
class C {
    var p: String
    init(p: String) {
        self.p = p
    }
}

let c1 = C(p: "one")
let c2 = C(p: "one")
let c3 = c1

print(c1 === c2) // false
print(c1 === c3) // true
print(c1 !== c2) // true
```

## 五、循环控制类

### 1. If - if let - if case let

```swift
// if
let s = "hi"
if s.isEmpty {
    print("String is Empty")
} else {
    print("String is \(s)")
}

// 三元条件
s.isEmpty ? print("String is Empty again") : print("String is \(s) again")

// if let-else
func f(s: String?) {
    if let s1 = s {
        print("s1 is \(s1)")
    } else {
        print("s1 is nothing")
    }
    // nil-coalescing
    let s2 = s ?? "nothing"
    print("s2 is \(s2)")
}
f(s: "something")
f(s: nil)

// if case let
enum E {
    case c1(String)
    case c2([String])
    
    func des() {
        switch self {
        case .c1(let string):
            print(string)
        case .c2(let array):
            print(array)
        }
    }
}

E.c1("enum c1").des()
E.c2(["one", "two", "three"]).des()
```

### 2. Guard guard, guard let

更好地处理异常情况

```swift
// guard
func f1(p: String) -> String {
    guard p.isEmpty != true else {
        return "Empty string."
    }
    return "String \(p) is not empty."
}

print(f1(p: "")) // Empty string.
print(f1(p: "lemon")) // String lemon is not empty.

// guard let
func f2(p1: String?) -> String {
    guard let p2 = p1 else {
        return "Nil."
    }
    return "String \(p2) is not nil."
}

print(f2(p1: nil)) // Nil.
print(f2(p1: "lemon")) // String lemon is not nil.
```

### 3. 遍历 For-in

```swift
// 基本使用
var sun = 0
for item in 1...10 {
    // 注意：item是常量，无法修改
    sun += item
}
// sun = 55

//忽略item
for _ in 1...5 {
    print("for in")
}

// for + while 偶数相加
var sum = 0
for item in 1...10 where item % 2 == 0 {
    sum += item
}
// sun = 30

//集合遍历
var arr = [1,2,3,4,5]
// 1. for in 循环
for item in arr {
    print(item)
}
// 2. enumerated
for (index, item) in arr.enumerated() {
    print("index \(index), item\(item)") // index 0, item1
}
// 3. forEach
arr.forEach { item in
    print(item)
}

// 字典 for in，遍历是无序的
let dic = [
    "one": 1,
    "two": 2,
    "three": 3
]

for (k, v) in dic {
    print("key is \(k), value is \(v)")
}

// stride
for i in stride(from: 10, through: 0, by: -2) {
    print(i)
}
/*
 10
 8
 6
 4
 2
 0
 */
```

### 4. while循环

```swift
// while
var i1 = 10
while i1 > 0 {
    print("positive even number \(i1)")
    i1 -= 2
}

// repeat while
var i2 = 10
repeat {
    print("positive even number \(i2)")
    i2 -= 2
} while i2 > 0
```



### 5. Switch

```swift
func f1(pa: String, t:(String, Int)) {
    var p1 = 0
    var p2 = 10
    switch pa {
    case "one":
        p1 = 1
    case "two":
        p1 = 2
        fallthrough // 继续到下个 case 中
    default:
        p2 = 0
    }
    print("p1 is \(p1)")
    print("p2 is \(p2)")
    
    // 元组
    switch t {
    case ("0", 0):
        print("zero")
    case ("1", 1):
        print("one")
    default:
        print("no")
    }
}

f1(pa: "two", t:("1", 1))
/*
 p1 is 2
 p2 is 0
 one
 */

// 枚举
enum E {
    case one, two, three, unknown(String)
}

func f2(pa: E) {
    var p: String
    switch pa {
    case .one:
        p = "1"
    case .two:
        p = "2"
    case .three:
        p = "3"
    case let .unknown(u) where Int(u) ?? 0 > 0 : // 枚举关联值，使用 where 增加条件
        p = u
    case .unknown(_):
        p = "negative number"
    }
    print(p)
}

f2(pa: E.one) // 1
f2(pa: E.unknown("10")) // 10
f2(pa: E.unknown("-10")) // negative number
```

### 6. 循环的嵌套与退出

```swift
var floors = [1,2]
var rooms = [11, 22]
for floor in floors {
    for room in rooms {
        print("floor: \(floor), room: \(room)")
    }
}
```

使用 break 结束遍历，使用 continue 跳过当前作用域，继续下个循环

```swift
for floor in floors {
    if floor == 1 {
        continue
    }
    for room in rooms {
        if room == 22 {
            // 终止内层循环
            break
        }
        print("floor: \(floor), room: \(room)")
    }
}
```



## 六、集合

### 1. 数组

*数组是有序集合*

- 基本使用

```swift
//数组声明
var intArr = [1,2,3]
print(type(of: intArr)) // Array<Int>
var intArr2: [Int] = [4,5,6]

//空数组
var intArr3: [Int] = []
var intArr4 = [Int]()

//下标访问
intArr[0] // 1
intArr[intArr.count - 1] // 3

//添加
intArr.append(4) // [1,2,3,4]
intArr += [4,11] // [1,2,3,4,4,11]

//获取前n个元素，后n个元素，中间元素
let firstThree = intArr.prefix(3) // [1,2,3]
let lastTwo = intArr.suffix(2) // [4,11]
let midThree = intArr[1...3] // [2,3,4]

//插入
intArr.insert(0, at: 0)

//删除
intArr.remove(at: 4)
intArr.removeAll()
intArr = []

//判断是否为空
intArr.isEmpty // true
//元素个数
intArr2.count // 3
//首个元素
intArr2.first //4
intArr2.last //6

//判断是否包含元素
intArr2.contains(4) // true

//交换两个元素下标 [4,5,6]
intArr2.swapAt(1, 2) // [4,6,5]
```



```swift
let a1 = ["one", "two", "three"]
let a2 = ["three", "four"]

// 找两个集合的不同
let dif = a1.difference(from: a2) // swift的 diffing 算法在这 http://www.xmailserver.org/diff2.pdf swift实现在  swift/stdlib/public/core/Diffing.swift
for c in dif {
    switch c {
    case .remove(let o, let e, let a):
        print("offset:\(o), element:\(e), associatedWith:\(String(describing: a))")
    case .insert(let o, let e, let a):
        print("offset:\(o), element:\(e), associatedWith:\(String(describing: a))")
    }
}
/*
 remove offset:1, element:four, associatedWith:nil
 insert offset:0, element:one, associatedWith:nil
 insert offset:1, element:two, associatedWith:nil
 */
let a3 = a2.applying(dif) ?? [] // 可以用于添加删除动画
print(a3) // ["one", "two", "three"]
```

dif 有第三个 case 值 .insert(let offset, let element, let associatedWith) 可以跟踪成对的变化，用于高级动画。

从数组中随机取一个元素

```swift
print(a0.randomElement() ?? 0)
```

数组排序

```swift
// 排序
struct S1 {
    let n: Int
    var b = true
}

let a4 = [
    S1(n: 1),
    S1(n: 10),
    S1(n: 3),
    S1(n: 2)
]
let a5 = a4.sorted { i1, i2 in
    i1.n < i2.n
}
for n in a5 {
    print(n)
}
/// S1(n: 1)
/// S1(n: 2)
/// S1(n: 3)
/// S1(n: 10)

let a6 = [1,10,4,7,2]
print(a6.sorted(by: >)) // [10, 7, 4, 2, 1]
```

可以加到数组扩展中，通过扩展约束能够指定特定元素类型的排序，代码如下：

```swift
extension Array where Element == Int {
    // 升序
    func intSortedASC() -> [Int] {
        return self.sorted(by: <)
    }
    // 降序
    func intSortedDESC() -> [Int] {
        return self.sorted(by: <)
    }
}

print(a6.intSortedASC()) // 使用扩展增加自定义排序能力
```

在数组中检索满足条件的元素，代码如下：

```swift
// 第一个满足条件了就返回
let a7 = a4.first {
    $0.n == 10
}
print(a7?.n ?? 0)

// 是否都满足了条件
print(a4.allSatisfy { $0.n == 1 }) // false
print(a4.allSatisfy(\.b)) // true

// 找出最大的那个
print(a4.max(by: { e1, e2 in
    e1.n < e2.n
}) ?? S1(n: 0))
// S1(n: 10, b: true)

// 看看是否包含某个元素
print(a4.contains(where: {
    $0.n == 7
}))
// false
```

一些切割数组的方法。

```swift
// 切片
// 取前3个，并不是直接复制，对于大的数组有性能优势。
print(a6[..<3]) // [1, 10, 4] 需要做越界检查
print(a6.prefix(30)) // [1, 10, 4, 7, 2] 不需要做越界检查，也是切片，性能一样

// 去掉前3个
print(a6.dropFirst(3)) // [7, 2]
```

prefix(while:) 和 drop(while:) 方法，顺序遍历执行闭包里的逻辑判断，满足条件就返回，遇到不匹配就会停止遍历。prefix 返回满足条件的元素集合，drop 返回停止遍历之后那些元素集合。

```swift
let a8 = [8, 9, 20, 1, 35, 3]
let a9 = a8.prefix {
    $0 < 30
}
print(a9) // [8, 9, 20, 1]
let a10 = a8.drop {
    $0 < 30
}
print(a10) // [35, 3]
```

比 filter 更高效的删除元素的方法 removeAll

```swift
// 删除所有不满足条件的元素
var a11 = [1, 3, 5, 12, 25]
a11.removeAll { $0 < 10 }
print(a11) // [4, 3, 1, 3, 3] 随机

// 创建未初始化的数组
let a12 = (0...4).map { _ in
    Int.random(in: 0...5)
}
print(a12) // [0, 3, 3, 2, 5] 随机
```

`#if` 用于后缀表达式

```swift
// #if 用于后缀表达式
let a13 = a11
#if os(iOS)
    .count
#else
    .reduce(0, +)
#endif
print(a13) //37
```

### 2. 字典

字典是无序集合，键值对应。

```swift
// 1. 字典创建
var dic1 : [String: Int] = [:]
dic1["Jame"] = 21
dic1["Rose"] = 22
print(dic1) // ["Rose": 22, "Jame": 21]
var dic2 = [String: Int]()
dic2["Jame"] = 21
print(dic2) // ["Jame": 21]

// 2. 遍历
// 2.1. for in 循环
for (key, value) in dic1 {
    print("\(key) === \(value)")
}
// 2.2. dictionary.forEach
dic1.forEach { (key, value) in
    print("\(key) === \(value)")
}
// 2.3. dictionary.keys, dictionary.values
for name in dic1.keys {
    print(name)
}

// 3. 字典的读取
//读取值
let firstNameAge = dic1["Jame"]
let noNameAge = dic1["no"] // nil
//if判空
if let hasNameAge = firstNameAge {
    print(hasNameAge)
}
//默认值
let secondStudent = dic1["Jeck"] ?? 23
let thirdStudent = dic1["Tom", default: 23]
//判断是否为空
print(dic1.isEmpty) // false
//键值对数量
print(dic1.count) // 2
//是否包含 建
if dic1.contains(where: { $0.key == "Jame" }) {
    print("jame")
} else {
    print("Not Found")
}
```



```swift
var d1 = [
    "k1": "v1",
    "k2": "v2"
]
d1["k3"] = "v3"
d1["k4"] = nil
print(d1) // ["k2": "v2", "k3": "v3", "k1": "v1"]

for (k, v) in d1 {
    print("key is \(k), value is \(v)")
}
/*
 key is k1, value is v1
 key is k2, value is v2
 key is k3, value is v3
 */
 
if d1.isEmpty == false {
    print(d1.count) // 3
}

// mapValues
let d2 = d1.mapValues {
    $0 + "_new"
}
print(d2) // ["k2": "v2_new", "k3": "v3_new", "k1": "v1_new"]

// 对字典的值或键进行分组
let d3 = Dictionary(grouping: d1.values) {
    $0.count
}
print(d3) // [2: ["v1", "v2", "v3"]]

// 从字典中取值，如果键对应无值，则使用通过 default 指定的默认值
d1["k5", default: "whatever"] += "."
print(d1["k5"] ?? "") // whatever.
let v1 = d1["k3", default: "whatever"]
print(v1) // v3

// compactMapValues() 对字典值进行转换和解包。可以解可选类型，并去掉 nil 值
let d4 = [
    "k1": 1,
    "k2": 2,
    "k3": nil
]
let d5 = d4.mapValues { $0 }
let d6 = d4.compactMapValues{ $0 }
print(d5)
// ["k3": nil, "k1": Optional(1), "k2": Optional(2)]
print(d6)
// ["k1": 1, "k2": 2]
```

### 3. Set

Set 是无序集合，元素唯一

```swift
//Set
// 1. 基本使用
var emptySet: Set<Int> = []
emptySet.insert(1)
emptySet.insert(2)
emptySet.insert(1)
print(emptySet) // [1,2]
let removeSet = emptySet.remove(2) // 2
let removeNilSet = emptySet.remove(3) // nil
print(emptySet.count) // 1
print(emptySet.contains(1)) // true

// 2. 常用api => 以下只会生成新Set不会修改原数据
var newSet: Set<Int> = [1,2,3,4,5]
let resultOne = newSet.intersection(emptySet) // 交集 [1]
let resultTwo = newSet.symmetricDifference(emptySet) // 非交集部分 [2,3,4,5]
let resultThree = newSet.union(emptySet) // 合集 [1,2,3,4,5]

// 3. 常用api => x修改原数据
var changeSet: Set<Int> = [0, 1]
changeSet.formIntersection(newSet) // [1]
```



```swift
let s0: Set<Int> = [2, 4]
let s1: Set = [2, 10, 6, 4, 8]
let s2: Set = [7, 3, 5, 1, 9, 10]

let s3 = s1.union(s2) // 合集
let s4 = s1.intersection(s2) // 交集
let s5 = s1.subtracting(s2) // 非交集部分
let s6 = s1.symmetricDifference(s2) // 非交集的合集
print(s3) // [4, 2, 1, 7, 3, 10, 8, 9, 6, 5]
print(s4) // [10]
print(s5) // [8, 4, 2, 6]
print(s6) // [9, 1, 3, 4, 5, 2, 6, 8, 7]

// s0 是否被 s1 包含
print(s0.isSubset(of: s1)) // true
// s1 是否包含了 s0
print(s1.isSuperset(of: s0)) // true

let s7: Set = [3, 5]
// s0 和 s7 是否有交集
print(s0.isDisjoint(with: s7)) // true

// 可变 Set
var s8: Set = ["one", "two"]
s8.insert("three")
s8.remove("one")
print(s8) // ["two", "three"]
```



## 七、类和结构体

### 1. 类

类可以定义属性、方法、构造器、下标操作。类使用扩展来扩展功能，遵循协议。类还以继承，运行时检查实例类型。

```swift
 class C {
     var p: String
     init(_ p: String) {
         self.p = p
     }
     
     // 下标操作
     subscript(s: String) -> String {
         get {
             return p + s
         }
         set {
             p = s + newValue
         }
     }
 }
 
 let c = C("hi")
 print(c.p)
 print(c[" ming"])
 c["k"] = "v"
 print(c.p)
```

### 2. 结构体

结构体是值类型，可以定义属性、方法、构造器、下标操作。结构体使用扩展来扩展功能，遵循协议。

```swift
struct S {
    var p1: String = ""
    var p2: Int
}

extension S {
    func f() -> String {
        return p1 + String(p2)
    }
}

var s = S(p2: 1)
s.p1 = "1"
print(s.f()) // 11
```

### 3. 属性

类、结构体或枚举里的变量常量就是他们的属性。

```swift
struct S {
    static let sp = "类型属性" // 类型属性通过类型本身访问，非实例访问
    var p1: String = ""
    var p2: Int = 1
    // cp 是计算属性
    var cp: Int {
        get {
            return p2 * 2
        }
        set {
            p2 = newValue + 2
        }
    }
    // 只有 getter 的是只读计算属性
    var rcp: Int {
        p2 * 4
    }
}
print(S.sp)
print(S().cp) // 2
var s = S()
s.cp = 3
print(s.p2) // 5
print(S().rcp) // 4
```

willSet 和 didSet 是属性观察器，可以在属性值设置前后插入自己的逻辑处理。

键路径表达式作为函数

```swift
struct S2 {
    let p1: String
    let p2: Int
}

let s2 = S2(p1: "one", p2: 1)
let s3 = S2(p1: "two", p2: 2)
let a1 = [s2, s3]
let a2 = a1.map(\.p1)
print(a2) // ["one", "two"]
```

### 4. 方法

```swift
```



```swift
enum E: String {
    case one, two, three
    func showRawValue() {
        print(rawValue)
    }
}

let e = E.three
e.showRawValue() // three

// 可变的实例方法，使用 mutating 标记
struct S {
    var p: String
    mutating func addFullStopForP() {
        p += "."
    }
}
var s = S(p: "hi")
s.addFullStopForP()
print(s.p)

// 类方法
class C {
    class func cf() {
        print("类方法")
    }
}
```

static和class关键字修饰的方法类似 OC 的类方法。static 可以修饰存储属性，而 class 不能；class 修饰的方法可以继承，而 static 不能。在协议中需用 static 来修饰。

静态下标方法

```swift
// 静态下标
struct S2 {
    static var sp = [String: Int]()
    
    static subscript(_ s: String, d: Int = 10) -> Int {
        get {
            return sp[s] ?? d
        }
        set {
            sp[s] = newValue
        }
    }
}

S2["key1"] = 1
S2["key2"] = 2
print(S2["key2"]) // 2
print(S2["key3"]) // 10
```

自定义类型中实现了 callAsFunction() 的话，该类型的值就可以直接调用。

```swift
// callAsFunction()
struct S3 {
    var p1: String
    
    func callAsFunction() -> String {
        return "show \(p1)"
    }
}
let s2 = S3(p1: "hi")
print(s2()) // show hi
```

### 5. 继承

类能继承另一个类，继承它的方法、属性等。

```swift
// 类继承
class C1 {
    var p1: String
    var cp1: String {
        get {
            return p1 + " like ATM"
        }
        set {
            p1 = p1 + newValue
        }
    }
    init(p1: String) {
        self.p1 = p1
    }
    func sayHi() {
        print("Hi! \(p1)")
    }
}

class C2: C1 {
    var p2: String
    init(p2: String) {
        self.p2 = p2
        super.init(p1: p2 + "'s father")
    }
}

C2(p2: "Lemon").sayHi() // Hi! Lemon's father

// 重写父类方法
class C3: C2 {
    override func sayHi() {
        print("Hi! \(p2)")
    }
}

C3(p2: "Lemon").sayHi() // Hi! Lemon

// 重写计算属性
class C4: C1 {
    override var cp1: String {
        get {
            return p1 + " like Out of the blade"
        }
        set {
            p1 = p1 + newValue
        }
    }
}

print(C1(p1: "Lemon").cp1) // Lemon like ATM
print(C4(p1: "Lemon").cp1) // Lemon like Out of the blade
```

通过 final 关键字可以防止类被继承，final 还可以用于属性和方法。使用 super 关键字指代父类。























