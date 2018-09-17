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
