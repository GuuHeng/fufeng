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
