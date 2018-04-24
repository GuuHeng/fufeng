# 我在RN学习实践中遇到的问题及解决
## question a.RN 在一系列环境配置后，运行AwesomeProject,在终端出现Error:
      
      error: bundling failed: TypeError: Cannot read property 'throwIfClosureRequired' of undefined

![image](https://txy-1256416399.cos.ap-beijing.myqcloud.com/rnerror02.png)

answer：

1、修改所在工程目录下的package.json文件
"babel-preset-react-native": "5.0.0" -> "4.0.0" 

2、npm install。


## question b.RN ...has not been registered...
![image](https://txy-1256416399.cos.ap-beijing.myqcloud.com/rnerror01.png)

answer: 同时存在两个运行的rn项目，关闭另一个正在运行的即可
