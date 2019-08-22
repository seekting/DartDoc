# 入门

## final 和 const区别

final 是运行时常量
const 是编译时常量
```dart {.line-numbers}
final time = new DateTime.now(); //Ok
const time = new DateTime.now(); //Error，new DateTime.now()不是const常量

```
## assert
在ide里可以选择开启和关闭assert检查
```dart {.line-numbers}
String str3 = "aaa";
assert(str3=="aaa1");

```

## 函数简写
``` =>expr;```等价于:```{return expr;}```
## 匿名函数

```dart {.line-numbers}
var sayHello = (name) => print("hello $name");
sayHello("Jim");
sayHello(0123);
```

## 内部函数

```dart {.line-numbers}
main(List<String> arguments) {
  int avg(int a, int b) {
    return (a + b) >> 1;
  }

  print("${avg(12, 14)}");
}

```

## 函数闭包

```dart {.line-numbers}
main(List<String> arguments) {
  invoke(2, (age) => print("age=$age"));
}

void invoke(int a, Function function) {
  function(a);
}

```

## 多参函数

```dart {.line-numbers}
FunX(int a, {int b, int c, String d}) {}


main(List<String> arguments) {
  FunX(4, b: 3, d: "xxx");
}

```
## 异常

好像打不出调用栈
```dart {.line-numbers}
try {
  breedMoreLlamas();
} on OutOfLlamasException {
  // A specific exception
  buyMoreLlamas();
} on Exception catch (e) {
  // Anything else that is an exception
  print('Unknown exception: $e');
} catch (e) {
  // No specified type, handles all
  print('Something really unknown: $e');
}

```

## 构造函数

```dart {.line-numbers}
class Point {
    num x;
    num y;
    num z;

    Point(this.x, this.y, z) { //第一个值传递给this.x，第二个值传递给this.y
            this.z = z;
    }

    Point.fromeList(var list): //命名构造函数，格式为Class.name(var param)
            x = list[0], y = list[1], z = list[2]{//使用冒号初始化变量
    }

    //当然，上面句你也可以简写为：
    //Point.fromeList(var list):this(list[0], list[1], list[2]);

     String toString() => 'x:$x  y:$y  z:$z';
}

void main() {
    var p1 = new Point(1, 2, 3);
    var p2 = new Point.fromeList([1, 2, 3]);
    print(p1);//默认调用toString()函数
}

class ImmutablePoint {
    final num x;
    final num y;
    const ImmutablePoint(this.x, this.y); // 常量构造函数
    static final ImmutablePoint origin = const ImmutablePoint(0, 0); // 创建一个常量对象不能用new，要用const
}

```

## 集合里的map

```dart {.line-numbers}
  Map a = Map();
  a["xxx"] = "xxx";
  a["xxb"] = "xxb";
  a.forEach((key, value) => print("key=${key},value=${value}"));

```

## 导包及part,partof

utils.dart
```dart {.line-numbers}
library utils;
part 'ioutils.dart';

int getVersion() {
  return 1;
}
```
ioutils.dart
```dart {.line-numbers}
part of 'utils.dart';

void close(){
  getVersion();

}

```
main.dart
```dart {.line-numbers}
import 'package:DartStudy/utils.dart';
main(List<String> arguments) {
  close();
}


```

