# flutter 小知识点

## windows安装问题处理 https://blog.csdn.net/weixin_40841731/article/details/109072564

## 类型转换

   String转Number，使用parse：
   ```
   String temp = "123";
   var num = double.parse(temp); 
   ```
   
   Number转String，使用toString：
   ```
   var temp = 123;
   var str = temp.toString(); 
   ```

## 函数创建及调用

创建一个带有参数的函数

1、
```
创建：void writeFlutter(String baseLanguage) {print($baseLanguage$year)}

调用：writeFlutter("Dart");
打印：Dart
```
2、
```
增加一个可选参数year
可选参数用 [] 包含
调用时可选参数可传可不传，

创建：void writeFlutter(String baseLanguage, [String year]) {print($baseLanguage$year)}

调用：writeFlutter("Dart"); 或者 writeFlutter("Dart", "2020");
打印：Dart2020
```
3、
```
增加一个命名参数year
命名参数用 {} 包含
调用时命名参数一定要带上参数名
创建：void writeFlutter(String baseLanguage, {String year}) {print($baseLanguage$year)}
调用：writeFlutter("Dart", year: "2020");
打印：Dart2020
```
4、
```
增加一个参数year，设置默认值2020后，也可传可不传
创建：void writeFlutter(String baseLanguage, {String year="2020"}) {print($baseLanguage$year)}
调用：writeFlutter("Dart"); 
打印：Dart2020
```
5、
```
Widget的color和decoration不能共存
```

## 谨防Text溢出，UI黄色警告，加限制：maxLines或添在Container中或其他

## iOS集成flutter
```
出现
[!] Invalid `Podfile` file: cannot load such file -- ../my_flutter/.ios/Flutter/podhelper.rb.
是路径错误

当flutter项目和iOS项目是如此路径时
Desktop/iOSProject/my_flutter
Desktop/iOSProject/xx.xcodeproj

这里应该是这样：flutter_application_path = 'my_flutter/'
```

```
运行XCode时报出flutter_export_environment.sh: line 8: inherited: command not found，在多次编译运行可能会产生这个问题，
这时需要到flutter项目中flutter clean下，之后flutter packages get

```
