# 异步

## await

await 可以修饰一个方法，这个方法的返回值可以是Future<?> 也可以是非Future

### await 修饰返回非Future的method

```dart {.line-numbers}
testAsync1() async {
  print("seekting:testAsync1 begin:");
  String f = await fu1();
  print("seekting:testAsync1 end:");
  return f;
}

String fu1() {
  print("seekting:fu1:");
  return "fu1";
}

void main() {
  print("main begin");
  Future future = testAsync1();
  future.then((value) {
    print("future then value$value");
  });
  print("main end");
}
```

输出:
```c {.line-numbers}
main begin
seekting:testAsync1 begin:
seekting:fu1:
main end
seekting:testAsync1 end:
future then valuefu1

```

<video src="./await1.mp4" width="640" height="480"
controls="controls"></video>
 
得出来的结论是:
await修饰method会继续走进去，直到method调用结束之后"阻塞",这里的阻塞并非真正的阻塞,而是代码又跳出该testAsync1()方法,
然后执行testAsync1()以外的代码,future.then可以理解成往looper里扔一个消息，main走到"main end"后，
await修饰的fu1开始要返回值给f,然后testAsync1 end:，最后future.then拿到回调
