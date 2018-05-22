# Bootstrap-region-selection
This is a component of a multi-select region in Bootstrap.
这是一个可多选的城市-区域关联型区域选择

# let me show you<br/> 一睹为快

Please click the picture. 
点击看大图会好点。
## Demo
![My project demo 1](https://raw.githubusercontent.com/xuzijie1995/Bootstrap-region-selection/master/images/screenshot_1.png)

## My Distribution template<br/> 我的配送模板案例
I use this selection in my project. And it has other functional requirements as well.<br/>
我在自己的项目中使用了这个组件，当然它还具备其他需求下的功能<br/>
###案例图1
![My project demo 2](https://raw.githubusercontent.com/xuzijie1995/Bootstrap-region-selection/master/images/screenshot_2_2.png)
----
###案例图2
![My project demo 3](https://raw.githubusercontent.com/xuzijie1995/Bootstrap-region-selection/master/images/screenshot_4.png)
<br/>
+ 1.Select Parent Address(Parent)，all Parent's(Children) children **which belong to Parent now** will be selected.Select all Children,their Parent will be selected.Click the name of Parent will show Parent's children,but nothing will be changed.
+ 2.All Children can be selected only one time in every Distribution template.The selected Children will be kicked out from the other setting lines in the Distribution template. And All Children are selected without being kicked out in other setting lines, the Address Name in the setting line will show the Parent's Name.See 2 srceenshots above.<br/>Maybe I should change the demo into English :P.
+ 1.一级地址“勾选”将影响其**当前从属**的所有对应二级地址，点击一级名称会显示对应二级地址，但不会影响二级地址，全选二级地址，对应一级地址也会被“勾选”
+ 2.在同一个配送模板中,所有二级地址只会出现一次，如上截图所示，在新的配送区域行中，已被选择的区域会被剔除，而且，全选一级地址从属的所有地址,同时，一级地址下的二级地址没有在其他配置行中被剔除，那么将会显示一级地址名称而非全被的二级地址名称,案例图2所示

# The setting code <br/> 代码

## Asynchronous data <br/> 异步数据

```Parent data
{"data":[
{"id":"11","parent_id":"0","name":"北京"},
{"id":"12","parent_id":"0","name":"天津"},
{"id":"13","parent_id":"0","name":"河北"},
{"id":"14","parent_id":"0","name":"山西"},
{"id":"15","parent_id":"0","name":"内蒙古"},
{"id":"21","parent_id":"0","name":"辽宁"},
{"id":"22","parent_id":"0","name":"吉林"},
{"id":"23","parent_id":"0","name":"黑龙江"},
{"id":"31","parent_id":"0","name":"上海"},
...
]}
```
```Children data
{"data":
{
...,
"32":[{"id":"3201","parent_id":"32","name":"南京"},{"id":"3202","parent_id":"32","name":"无锡"},{"id":"3203","parent_id":"32","name":"徐州"},{"id":"3204","parent_id":"32","name":"常州"},{"id":"3205","parent_id":"32","name":"苏州"},{"id":"3206","parent_id":"32","name":"南通"},{"id":"3207","parent_id":"32","name":"连云港"},{"id":"3208","parent_id":"32","name":"淮安"},{"id":"3209","parent_id":"32","name":"盐城"},{"id":"3210","parent_id":"32","name":"扬州"},{"id":"3211","parent_id":"32","name":"镇江"},{"id":"3212","parent_id":"32","name":"泰州"},{"id":"3213","parent_id":"32","name":"宿迁"}],
"33":[{"id":"3301","parent_id":"33","name":"杭州"},{"id":"3302","parent_id":"33","name":"宁波"},{"id":"3303","parent_id":"33","name":"温州"},{"id":"3304","parent_id":"33","name":"嘉兴"},{"id":"3305","parent_id":"33","name":"湖州"},{"id":"3306","parent_id":"33","name":"绍兴"},{"id":"3307","parent_id":"33","name":"金华"},{"id":"3308","parent_id":"33","name":"衢州"},{"id":"3309","parent_id":"33","name":"舟山"},{"id":"3310","parent_id":"33","name":"台州"},{"id":"3311","parent_id":"33","name":"丽水"}],
...
}}
```
+ I get all Parent Address And Children Address for one time from ajax.Every Children Address has 'parent_id' which can be used to find its Parent Address.<br/>
+ 我请求的数据包含所有一级地址与二级地址，二级地址通过内部的'parent_id'对应一级地址.




to be continue
