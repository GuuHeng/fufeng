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

## Mac安装Android Studio4.1版本，4.0以上版本在flutter doctor时会报✗ Flutter plugin not installed; this adds Flutter specific functionality.

Android Studio (4.1) 的插件位置换成了
```
~/Library/Application\ Support/Google/AndroidStudio4.1/plugins，
```
而老版本的位置为
```
~/Library/Application\ Support/AndroidStudio4.1
```
所以用 flutter doctor 这个命令去检测时，还是会去原来的位置查找这两个插件找不到。

解决办法:给新目录添加软连接

```
ln -s ~/Library/Application\ Support/Google/AndroidStudio4.1/plugins ~/Library/Application\ Support/AndroidStudio4.1
```

## iOS集成flutter module

```
flutter_application_path = '../FlutterModule/'
load File.join(flutter_application_path, '.ios', 'Flutter', 'podhelper.rb')

install_all_flutter_pods(flutter_application_path)

```


```
podfile中使用
      eval(File.read(File.join(flutter_application_path, '.ios', 'Flutter', 'podhelper.rb')),binding)
在执行pod install时，会报
[!] Invalid `Podfile` file: /Users/huheng/Desktop/projects/sm/Flutter/Generated.xcconfig must exist. If you're running pod install manually, make sure flutter pub get is executed first.
在百度、google了半天，也清理了下pod，还是解决未果；
改用  
load File.join(flutter_application_path, '.ios', 'Flutter', 'podhelper.rb')
pod install执行成功

```
