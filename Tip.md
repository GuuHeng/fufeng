# 通过NSNumberFormatter进行json数据精度问题的处理
  如果遇到json数据中有double等数据形式时，在转模型为NSNumber，NSString时，会有概率出现精度问题，例如：2.75 -> 2.74999999999等，
  所以在进行text文本显示前，需要进行精度处理，通过NSNumberFormatter进行处理
  
    ```  NSNumberFormatter *formatter = [[NSNumberFormatter alloc] init];
         formatter.numberStyle = NSNumberFormatterDecimalStyle;
         NSString *number = [formatter stringFromNumber:num];
    ```
