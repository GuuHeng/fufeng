# Xib在iOS10 和 iOS11中高度问题

xib中设置好约束后，分别启动iOS10 和 iOS11模拟器，在iOS11上能自适应高度，无须进行代码层面的编辑即可，完全显示想要的界面；而在iOS10上会是默认高度，无法实现自适应高度，所以需要在代码中return确定的高度来适配iOS10

目前知道可能应该是系统版本的原因吧



## storyboard viewcontroller传值 

  使用storyboard进行开发，控制器间连线跳转如果需要传值，需进行如下操作
  
  1. 选中两个controller间的连线并设置identifier
  2. 假如A controller向B controller跳转，则在A controller的 .swift中重写函数
  
    func prepare(for segue: UIStoryboardSegue, sender: Any?)
    
  · 最简单最基本的传值如 Demo1: 
  
  
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
    
    
  · 控制器中 tableview 点击 cell 如何进行跳转传值
    在纯代码创建的控制器中通过
    
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) 
    
跳转传值，但是在storyboard里建的viewcontroller中通过这个方法已经不能实现跳转了

tableview 的点击事件调用的方法传递分为三步
   1、 先是
   
    func tableView(_ tableView: UITableView, willSelectRowAt indexPath: IndexPath)
     
   2、之后是调用这个方法，并进行跳转了，所以进行 data获取需要在前一步（即是第1步）中进行，并在当前方法进行赋值传递
   
    func prepare(for segue: UIStoryboardSegue, sender: Any?)
     
   3、 最后才是下面这个方法，因为已经在第2步跳转了，所以在下面这个方法进行获取data并赋值传递是行不通的
   
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath)

· 需要进行条件判断是否跳转，该如何操作呢
  调用

    func shouldPerformSegue(withIdentifier identifier: String, sender: Any?) -> Bool 
        
  该方法进行条件判断，满足条件return true，不满足条件return false
  
  Demo:
```var isTrue: Bool = false
    var dataSource: Array<String> = ["q", "w", "e", "r"]
    var selectedString: String = "random"
    
    // 该方法中获取需要传递的值
    func tableView(_ tableView: UITableView, willSelectRowAt indexPath: IndexPath) -> IndexPath? {
        if indexPath.row < (dataSource.count)! {
            let rowString = dataSource[indexPath.row]
            selectedString = rowString
            if rowString = "e" {
               isTrue = true
            }
        }
        return indexPath
    }
   
    // 该方法进行判断是否满足条件并跳转
    override func shouldPerformSegue(withIdentifier identifier: String, sender: Any?) -> Bool {
        if identifier == "A" {
            if isTrue == true {
                return true
            }
        }
        return false
    }
    
    // 该方法进行传值
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        if segue.identifier == "A" {
            let vc: BViewController = segue.destination as! BViewController
            vc.title = selectedString
        }
    }

