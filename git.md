## git使用

### issue

1、使用sourcetree进行pull操作后，在打开冲突文件去除“<<<<<” "====="">>>>>"后，project工程文件还是不能打开

2、这时候应该仔细查看在“<<<” ">>>""==="符号之间的冲突代码，类似如下的情况时，不是简单去除“<<<<<” "====="">>>>>"就能解决冲突的（我就是遇到了这种情况。。。）

``` 
    <<<<<
    3301023003240240E0F12323 /* BController */ = {
    =====
    331C316A20E62FE40068005E /* AController */ = {
    >>>>>
			isa = PBXGroup;
			children = (
				331C316B20E630150068005E /* UNMailContactorTableViewCell.h */,
				331C316C20E630150068005E /* UNMailContactorTableViewCell.m */,
				331C316D20E630150068005E /* UNMailContactorTableViewCell.xib */,
			);
			path = UNContactorsChooseViewController;
			sourceTree = "<group>";
		};
```
