# cell使用masonry进行AutoLayout时，避免在layoutSubviews中添加约束代码

作为一名iOS Objective-C coder，使用UITableView相当频繁，基本的优化方面几乎都有接触过，网上的众多帖子也有相应的优化思路，我现在记录下一个很小的东西，
方便以后的查看（不用那么费脑）

1. 如果在layoutSubviews进行代码约束，当我们滑动tableview时，cell的layoutSubviews会频繁调用，而我们知道函数调用是需要一定的资源开销的，
  这会增加CPU不必要的工作量
2. e如果进行代码约束，我们可以进行在cell创建时，所有视图被addSubview：之后进行约束的添加工作。
3. 对于一些不复杂的cell，我目前会将约束统一写进updateConstraints中，因为这是系统提供的更新约束的方法，然后在cell创建的最后调用updateFocusIfNeeded进行
  约束的添加

# YYLabel 刷新闪烁问题处理

        _contentLabel.fadeOnAsynchronouslyDisplay = NO;
        _contentLabel.fadeOnHighlight = NO;

# tableview 更新数据到第二页时，不手动下拉刷新，而点击事件中调用beginRefresh刷新，tableview会回不到顶部问题
     应该是beginRefresh时，tableview回到顶部，存在估算高度造成整体height不准，回到顶部不准。
     1、一定要关闭估算 estimatedRowHeight；self.tableView.estimatedRowHeight = 0.0;
     2、不使用系统自动约束UITableViewAutomaticDimension
     3、要自己计算cellheight
     
     
     
     
