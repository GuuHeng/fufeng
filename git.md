## git使用

### issue

1、使用sourcetree进行pull操作后，在打开冲突文件去除“<<<<<” "====="">>>>>"后，（project工程文件还是不能打开）而愚蠢的我给直接提交并推送上去了。。。

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

project文件打不开后，因为已经提交了，我只能回退版本，重置、提交回滚到之前版本，再重新添加进自己开发的文件，这个时候进行提交前的拉取会拉取到出问题的记录版本。没有办法，重新回退，继续操作。。。 总之，使用sourcetree并没有解决掉这个问题

这时候就该提现命令行的强大了，使用强推git push -f，不进行拉取，直接跳过问题版本



