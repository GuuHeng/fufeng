# cocoapods制作公有库整理

下文代码都为 terminal commond:

### 第一步：
         
    注册cocoapods账号，
         
    a.修改your_email为自己的github账号邮箱
         
    b.修改your_name为想设置的名字
      
```
    pod trunk register your_email 'your_name' --verbose
```
    
    
  设置完后，邮箱会收到邮件，登录邮箱确认即可
  
### 第二步：确认之后
 
 ```
    pod trunk me
 ```
    
### 第三步：
在github上创建一个空仓库，例如PodDemo,确保包含LICENSE，README.md文件，然后将PodDemo clone到本地
  
### 第四步：
在本地PodDemo文件夹中，创建工程项目代码，然后git同步到github仓库
  
### 第五步：
创建.podspec，例创建PodDemo.podspec，（.podspec是用ruby的配置文件，描述项目信息）
     
     pod spec create PodDemo
     
     
### 第六步：在.podspec文件中进行项目配置修改
    
``` Pod::Spec.new do |s|
     s.name         = "PodDemo" # 项目名称
     s.version      = "0.0.1"  # 版本号 与 你仓库的 标签号tag 对应
     s.license      = { :type => "MIT", :file => "LICENSE" }          # 开源证书
     s.summary      = "my PodDemo test" # 项目简介

     s.homepage     = "https://github.com/GuuHeng/HHPopAnimation" # 你的主页
     s.source       = { :git => "https://github.com/GuuHeng/HHPopAnimation.git", :tag => "#{s.version}" } #你的仓库地址，不能用SSH地址
     s.source_files = "PodDemo/*.{h,m}" # 你代码的位置， PodDemo/*.{h,m} 表示 PodDemo 文件夹下所有的.h和.m文件
     s.requires_arc = true # 是否启用ARC
     s.platform     = :ios, "7.0" #平台及支持的最低版本
     s.frameworks   = "UIKit", "Foundation" #支持的框架
     # s.dependency   = "AFNetworking" # 依赖库
  
     # User
     s.author             = { "HuHeng" => "huheng080309@163.com" } # 作者信息
     s.social_media_url   = "https://github.com/GuuHeng" # 个人主页

    end
```
    
### 第七步：
修改完 .podspec后，验证其正确性，终端键入
     
```
    pod lib lint
```
     
   
   验证成功会出现
```    
    -> PodDemo (0.0.1)
    PodDemo passed validation
``` 
### 第八步：
给仓库打标签，1.创建表情，2.推送到远程
```
    git tag -a 0.0.1 -m '打tag，这里是标签说明'
    git push origin --tags
```
### 第九步：发布
```
    pod trunk push PodDemo.podspec
```
    
如果成功了，会出现以下字样
```
    Updating spec repo `master`
    Validating podspec
     -> PodDemo (0.0.1)

    Updating spec repo `master`

     --------------------------------------------------------------------------------
    🎉  Congrats

    🚀  BYPhoneNumTF (1.0.0) successfully published
    📅  March 7th, 01:39
    🌎  https://cocoapods.org/pods/BYPhoneNumTF
    👍  Tell your friends!
```
   
### 第十步：使用
```
    pod setup
    ...
```
    
### 第十一步：更新维护
1、代码修改更新后，需要修改.podspec中的版本号version


2、打标签，推送远程 > 第八步


3、
```
   pod trunk push PodDemo.podspec
```

### 如果pod search 不到库，则可以先执行
```
   rm ~/Library/Caches/CocoaPods/search_index.json
```

### pod repo update --verbose报错error: RPC failed; curl 56 LibreSSL SSL_read: SSL_ERROR_SYSCALL, errno 54
```
   git config --global http.postBuffer 524288000
```

```执行pod命令时，报
/System/Library/Frameworks/Ruby.framework/Versions/2.6/usr/lib/ruby/2.6.0/universal-darwin20/rbconfig.rb:229: warning: Insecure world writable dir /usr/local/opt in PATH, mode 040777

处理：
sudo chmod go-w /usr/local/opt
sudo chmod 775 /usr/local

```
```
