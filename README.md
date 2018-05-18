# Bootstrap-region-selection
This is a component of a multi-select region in Bootstrap.
这是一个可多选的城市-区域关联型区域选择

# let me show you<br/> 一睹为快

Please click the picture. 
点击看大图会好点。
## Demo
![My project demo 1](https://raw.githubusercontent.com/xuzijie1995/Bootstrap-region-selection/master/images/screenshot_1.png)

## My Distribution template
I use this selection in my project. And it has other functional requirements as well.<br/>
我在自己的项目中使用了这个组件，当然它还具备其他需求下的功能<br/>
![My project demo 2](https://raw.githubusercontent.com/xuzijie1995/Bootstrap-region-selection/master/images/screenshot_2_2.png)
----
![My project demo 3](https://raw.githubusercontent.com/xuzijie1995/Bootstrap-region-selection/master/images/screenshot_4.png)
<br/>
+ 1.Select Parent Address(Parent)，all Parent's(Children) children **which belong to Parent now** will be selected.Select all Children,their Parent will be selected.Click the name of Parent will show Parent's children,but nothing will be changed.
+ 2.All Children can be selected only one time in every Distribution template.The selected Children will be kicked out from the other setting lines in the Distribution template. And All Children are selected without being kicked out in other setting lines, the Address Name in the setting line will show the Parent's Name.See 2 srceenshots above.<br/>Maybe I should change the demo into English :P.
+ 1.一级地址“勾选”将影响其**当前从属**的所有对应二级地址，点击一级名称会显示对应二级地址，但不会影响二级地址，全选二级地址，对应一级地址也会被“勾选”
+ 2.在同一个配送模板中,所有二级地址只会出现一次，如上截图所示，在新的配送区域行中，已被选择的区域会被剔除，而且，全选一级地址从属的所有地址,同时，一级地址下的二级地址没有在其他配置行中被剔除，那么将会显示一级地址名称而非全被的二级地址名称,如图上所示

