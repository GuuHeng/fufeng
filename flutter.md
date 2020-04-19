# flutter 小知识点

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
