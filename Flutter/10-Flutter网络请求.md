



# 一、Dart中的网络请求

Dart提供了`http`库，它是一个强大的HTTP客户端库，用于发送HTTP请求和处理响应。

在`pubspec.yaml`文件中添加`http`库的依赖：

```yaml
dependencies:
  http: ^0.13.3
```

使用`http`库中的`get`或`post`等方法发送HTTP请求。这些方法返回一个`Future`对象，表示异步操作。

```dart
import 'package:http/http.dart' as http;

void fetchPosts() async {
  var url = Uri.parse('https://example.com/api/posts');
  var response = await http.get(url);

  if (response.statusCode == 200) {
    // 请求成功，处理响应数据
    print(response.body);
  } else {
    // 请求失败，处理错误信息
    print('请求失败: ${response.statusCode}');
  }
}
```



# 二、Flutter中的网络请求

在Flutter中，我们可以使用`http`库进行网络请求，也可以使用更高级的网络请求库，如`dio`或`flutter_http`。这些库提供了更多功能和便捷的API，用于处理网络请求和响应。

在`pubspec.yaml`文件中添加`dio`库的依赖：

```yaml
dependencies:
  dio: ^4.0.4
```

然后，使用`dio`库中的方法发送HTTP请求。同样，这些方法也返回一个`Future`对象。

```dart
import 'package:dio/dio.dart';

void fetchPosts() async {
  var dio = Dio();
  var url = 'https://example.com/api/posts';

  try {
    var response = await dio.get(url);
    // 请求成功，处理响应数据
    print(response.data);
  } catch (e) {
    // 请求失败，处理错误信息
    print('请求失败: $e');
  }
}
```

了解更多：[dio库文档open in new window](https://pub.dev/packages/dio)



# 三、异步操作和错误处理

在进行网络请求时，我们需要注意异步操作和错误处理。由于网络请求是一个耗时的操作，我们应该使用`async`和`await`关键字来处理异步操作。这样可以确保在请求完成之前，不会阻塞应用程序的其他操作。

在处理网络请求时，我们还需要考虑错误处理。网络请求可能会失败，例如服务器返回错误状态码或网络连接中断。我们应该使用`try-catch`语句来捕获异常，并在出现错误时进行相应的处理。

# 四、解析和处理响应数据

一旦收到服务器的响应，我们通常需要解析和处理响应数据。常见的响应数据格式包括JSON、XML和HTML等。我们可以使用Flutter提供的JSON解析库，如`dart:convert`来解析JSON数据。

```dart
import 'dart:convert';

void handleResponse(String responseBody) {
  var jsonResponse = jsonDecode(responseBody);
  // 解析JSON数据并进行相应的处理
  print(jsonResponse['message']);
}
```

了解更多：[dart:convert库文档open in new window](https://api.flutter.dev/flutter/dart-convert/dart-convert-library.html)



# 五、Flutter请求封装

## 1. 设计要求

- 支持网络库插拔设计，不干扰业务层
- 简洁易用，支持配置进行请求
- Adapter 设计，扩展型强
- 统一异常和返回处理

![image-20240416212421481](./assets/image-20240416212421481.png)























































