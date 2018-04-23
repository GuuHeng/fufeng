RN 在一系列环境配置后，运行AwesomeProject
在终端出现Error:
      
      error: bundling failed: TypeError: Cannot read property 'throwIfClosureRequired' of undefined

解决：

1、修改所在工程目录下的package.json文件
"babel-preset-react-native": "5.0.0" -> "4.0.0" 

2、npm install。
