
1、今天让同事部署了一个vue页面，vite+vue3+js，结果访问地址后一片空白，但在资源中能看到assets中的css和js文件；
  而我本地nginx部署的测试是可以看到内容的，基于此我怀疑是不是nginx的config是不是配置漏了，翻了半天nginx文章也改了半天也无法成功。
   最终发现是我本地nginx配置的location一直是root根目录www下访问，而同事配置nginx上是次级目录访问，最终发现vue router中的模式是history，
   改为hash之后重新打包就可以了。
   
   以此谨记！！！本地调试是一回事，nginx部署后的是另一回事！！！两个需结合起来查问题！！！
