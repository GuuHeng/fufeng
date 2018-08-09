## UISwitch 使用selected，而不用on

    打开或者关闭UISwitch，如果使用属性 on 会造成UISwtich的SEL事件响应两次，在里面进行的一些操作会产生与预想不同的结果
    此时，应该使用父类UIControl下的selected属性，来改变UISwitch的打开或者关闭状态

👇这样会产生不同结果，触发两次
        
    - (IBAction)fingerPrintAction:(id)sender {
        self.fingerprintSwitch.on = !self.fingerprintSwitch.on;
        if (self.fingerprintSwitch.on) {
            self.gestureSwitch.on = NO;
            self.isHasSettedGesturePassword = YES;
        }
        [self.tableView reloadData];
        [self authTouchID];
    } 
    
👇这样才可以，只触发一次

    - (IBAction)fingerPrintAction:(id)sender {
        self.fingerprintSwitch.on = !self.fingerprintSwitch.on;
        if (self.fingerprintSwitch.on) {
            self.gestureSwitch.on = NO;
            self.isHasSettedGesturePassword = YES;
        }
        [self.tableView reloadData];
        [self authTouchID];
    }
    
    
    
