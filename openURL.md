# openURL.md
# 快速调起 拨打电话功能

`UIApplication.shared.openURL(_ url: URL)`
在APP需要使用电话功能时，一般会调用这个方法，然而这个方法存在局限性
在iOS 10.2以前，`UIApplication.shared.openURL(_ url: URL)`是可以快速调起选择弹窗，不存在延迟

但是在iOS 10.2以后，调用会在延迟数秒后才出现弹窗，这个就很不舒服了，所以在iOS 10.2以后我会启用另一个方法
```
open func open(_ url: URL, options: [String : Any] = [:], completionHandler completion: ((Bool) -> Swift.Void)? = nil)
```
这个方法在iOS 10.2以后会快速调起弹窗哦~ ~ ~
我开始做笔记了~
```
   func callPhone()
    {
        let telephone = "11111111"
        let telephoneString = "tel:\(telephone)"
        if #available(iOS 10.2, *)
        {
            UIApplication.shared.open(URL.init(string: telephoneString)!,
                                      options: [:],
                                      completionHandler: nil)
        }
        else
        {
            let alertC = UIAlertController.init(title: "拨打电话",
                                                message: telephone,
                                                preferredStyle: .alert)
            let ensureAction = UIAlertAction.init(title: "确定",
                                                  style: .default,
                                                  handler: { (alertAction) in
                                                    UIApplication.shared.openURL(URL.init(string: telephoneString)!)
            })
            
            let cancelAction = UIAlertAction.init(title: "取消",
                                                  style: .cancel,
                                                  handler: nil)
            alertC.addAction(ensureAction)
            alertC.addAction(cancelAction)
            
            self.present(alertC, animated: true, completion: nil)
        }
    }
```
