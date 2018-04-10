# runtime小记

iphoneX的出现，项目需要增加一些适配的X的图片，取名类似image_x.png

在修改了所需width、height后，为了不用区分机型调用imageName:方法，使用runtime黑魔法来解决

在以往使用method swizzling 中，替换的都是对象方法

现在要替换对象方法，在第一步获取类时有所变动，如下
    
    Class metaClass = object_getClass(class)；
