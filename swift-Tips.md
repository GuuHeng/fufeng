## 后台获取的图片字符串存在中文，使用kingfisher无法直接加载
解决方法：   

     addingPercentEncoding(withAllowedCharacters: .urlQueryAllowed)
    
    例：
    
    let imageString = "https://www.baidu.com/.../斯威夫特.png"
    cell.imageView.kf.setImage(with: URL.init(string: imageString.addingPercentEncoding(withAllowedCharacters: .urlQueryAllowed)!))
   
    
