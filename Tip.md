# 通过NSNumberFormatter进行json数据精度问题的处理
  如果遇到json数据中有double等数据形式时，在转模型为NSNumber，NSString时，会有概率出现精度问题，例如：2.75 -> 2.74999999999等，
  所以在进行text文本显示前，需要进行精度处理，通过NSNumberFormatter进行处理
  ```
     NSNumberFormatter *formatter = [[NSNumberFormatter alloc] init];
     formatter.numberStyle = NSNumberFormatterDecimalStyle;
     NSString *number = [formatter stringFromNumber:num];
  ```

# 使用HealthKit获取今日步数的权限问题
  第一次使用时，我先获取已知权限，再进行请求权限，发现这种是错误的；
  在健康APP中步数权限是关闭时，将它打开，再回到本APP中获取的权限是Deny的，与正常的权限管理存在差异，使用HealthKit就不要先获取已知权限了，而应该直接进行请求
  
  存在问题的：
```
   HKObjectType *stepCountType = [HKObjectType quantityTypeForIdentifier:HKQuantityTypeIdentifierStepCount];
   HKAuthorizationStatus status = [self.healthStore authorizationStatusForType:stepCountType];
    if (status == HKAuthorizationStatusSharingDenied) {
        return;
    }
    if (status == HKAuthorizationStatusSharingAuthorized) {
        return;
    }
    
    if (status == HKAuthorizationStatusNotDetermined) {
        [self.healthStore requestAuthorizationToShareTypes:nil readTypes:set completion:^(BOOL success, NSError * _Nullable error) {
        
            if (success) {
                [self readStepCount];
             } else {
                [self handleHealthAuthDenied];
             }
        }];
    }
```

   不存在问题的：
```
  HKObjectType *stepCountType = [HKObjectType quantityTypeForIdentifier:HKQuantityTypeIdentifierStepCount];
  [self.healthStore requestAuthorizationToShareTypes:nil readTypes:set completion:^(BOOL success, NSError * _Nullable error) {
        
        if (success) {
            [self readStepCount];
        } else {
            [self handleHealthAuthDenied];
        }
    }];
```

# 多工程依赖问题
## 我在开始多工程工作时，正常操作后，在Demo中没有问题，在项目里却出现问题“file not found”，在处理该问题时，发现应该是在项目里的子工程中加了个文件夹，由于多了一层文件路径，主工程在原有路径下查找不到文件。。。
主工程依赖子工程A时，如果引用A中文件出现“file not founded”，则可能头文件路径添加不完全的缘故。
如果A中存在文件夹，主工程中添加子工程A的文件路径时，如果只添加了最外层的文件夹路径，需要调整Header Search Paths的non-recursive为recursive，这样在主工程中引用A中文件时，会递归到A中的这个文件，bingo!


# UIAlertController 文字居中
```
// view: UIAlertController的视图
// message: 文本内容
// msgAlignment: 文本对齐方式
+ (void)enumrateSubviewsInView:(UIView *)view message:(NSString*)message msgAlignment:(NSTextAlignment)msgAlignment {
    NSArray *subViews = view.subviews;
    if (subViews.count == 0) {
        return;
    }
    for (NSInteger i = 0; i < subViews.count; i++) {
        UIView *subView = subViews[i];
        [self enumrateSubviewsInView:subView message:message msgAlignment:msgAlignment];
        
        if ([subView isKindOfClass:[UILabel class]]) {
            UILabel *label = (UILabel *)subView;
            if ([label.text isEqualToString:message]) {
                label.textAlignment = msgAlignment;
            }
        }
    }
}
```
             
# unicode和中文互转
```
//unicode转中文
NSString* strA = [@"%E4%B8%AD%E5%9B%BD"stringByReplacingPercentEscapesUsingEncoding:NSUTF8StringEncoding];

//中文转unicode
NSString *strB = [@"中国"stringByAddingPercentEscapesUsingEncoding:NSUTF8StringEncoding];


ios9之后

NSString *urlStr = @"url地址";

//中文转unicode
urlStr = [urlStr stringByAddingPercentEncodingWithAllowedCharacters:[NSCharacterSet URLQueryAllowedCharacterSet]];

//unicode转中文
urlStr = [urlStr stringByRemovingPercentEncoding];
```


# 上传AppStore问题 .../Demo.framework contains unsupported architectures '[x86_64,i386]'
  为了方便开发者使用，有的SDK将 i386 x86_64 armv7 arm64几个平台合并到一起，所以上传AppStore时需要移除i386 x86_64平台，方可提交
  
  在SDK路径下执行命令删除i386 x86_64平台：
    
    cd 目标framework
    # 使用lipo -info 可以查看包含的架构
    lipo -info AipBase.framework/AipBase  # Architectures in the fat file: Demo are: i386 x86_64 armv7 armv7s arm64
    # 移除x86_64, i386
    lipo -remove x86_64 Demo.framework/Demo -o Demo.framework/Demo
    lipo -remove i386 Demo.framework/Demo -o Demo.framework/Demo
    # 再次查看
    lipo -info Demo.framework/Demo # Architectures in the fat file: Demo are: armv7 armv7s arm64
  



# 字符串containsString:报错
    在实际需求中，对通讯录群组名称进行匹配搜索，群组名称字符串进行containsString:操作时，群组名称不只NSString，也会存在NSTaggedPointerString的情况，NSTaggedPointerString进行containsString:会直接报错（[NSTaggedPointerString rangeOfString:options:range:locale:]）
    我们需要将名称进行转换：
    NSMutableString *mutableString = [NSMutableString stringWithString:groupName];
    对mutableString进行containsString:操作

# 制作子工程静态库，swift不支持static library .a静态库的制作，需要改制作framework
