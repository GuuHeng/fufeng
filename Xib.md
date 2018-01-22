# Xib在iOS10 和 iOS11中高度问题

xib中设置好约束后，分别启动iOS10 和 iOS11模拟器，在iOS11上能自适应高度，无须进行代码层面的编辑即可，完全显示想要的界面；而在iOS10上会是默认高度，无法实现自适应高度，所以需要在代码中return确定的高度来适配iOS10

目前知道可能应该是系统版本的原因吧



## storyboard viewcontroller传值 

  使用storyboard进行开发，控制器间连线跳转如果需要传值，需进行如下操作
  1. 选中两个controller间的连线并设置identifier
  2. 假如A controller向B controller跳转，则在A controller的 .swift中重写函数
  
    func prepare(for segue: UIStoryboardSegue, sender: Any?)
    
  Demo1:
  
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
         if segue.identifier == "goA"
        {
            let AVC: AViewController = segue.destination as! AViewController
            A.flag = "1"
        }
        else if segue.identifier == "goB"
        {
            let B: BViewController = segue.destination as! BViewController
            B.flag = "1"
        }
    }
