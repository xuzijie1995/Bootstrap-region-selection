# Bootstrap-region-selection
This is a component of a multi-select region in Bootstrap.
这是一个可多选的城市-区域关联型区域选择

# let me show you<br> 一睹为快

Please click the picture. 
点击看大图会好点。
## Demo
![My project demo 1](https://raw.githubusercontent.com/xuzijie1995/Bootstrap-region-selection/master/images/screenshot_1.png)

## My Distribution template<br> 我的配送模板案例
I use this selection in my project. And it has other functional requirements as well.<br/>
我在自己的项目中使用了这个组件，当然它还具备其他需求下的功能<br/>
### 案例图1
![My project demo 2](https://raw.githubusercontent.com/xuzijie1995/Bootstrap-region-selection/master/images/screenshot_2_2.png)
----
### 案例图2
![My project demo 3](https://raw.githubusercontent.com/xuzijie1995/Bootstrap-region-selection/master/images/screenshot_4.png)
<br>
+ 1.Select Parent Address(Parent)，all Parent's(Children) children **which belong to Parent now** will be selected.Select all Children,their Parent will be selected.Click the name of Parent will show Parent's children,but nothing will be changed.
+ 2.All Children can be selected only one time in every Distribution template.The selected Children will be kicked out from the other setting lines in the Distribution template. And All Children are selected without being kicked out in other setting lines, the Address Name in the setting line will show the Parent's Name.See 2 srceenshots above.<br/>Maybe I should change the demo into English :P.
+ 1.一级地址“勾选”将影响其**当前从属**的所有对应二级地址，点击一级名称会显示对应二级地址，但不会影响二级地址，全选二级地址，对应一级地址也会被“勾选”
+ 2.在同一个配送模板中,所有二级地址只会出现一次，如上截图所示，在新的配送区域行中，已被选择的区域会被剔除，而且，全选一级地址从属的所有地址,同时，一级地址下的二级地址没有在其他配置行中被剔除，那么将会显示一级地址名称而非全被的二级地址名称,案例图2所示

# The setting code <br> 代码

## Asynchronous data <br> 异步数据

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
+ I get all Parent Address And Children Address for one time from ajax.Every Children Address has 'parent_id' which can be used to find its Parent Address.<br>
+ 我请求的数据包含所有一级地址与二级地址，二级地址通过内部的'parent_id'对应一级地址.

## Key Code <br> 关键代码
### 1.Create city-area checkboxs 二级与一级地址栏构建

```create City List
function createCityList(){//构建二级地址checkbox列表
	$removeProvinceList="";
	var content='';
	for(var i=0;i<Object.keys($cityGroup).length;i++){
		var pId=Object.keys($cityGroup)[i];
		var cityList="";
		for(var j=0;j<$cityGroup[pId].length;j++){
			if($removeCityList.indexOf($cityGroup[pId][j]['id'])<0){//剔除非本行数据选择地区的已选区域
				var checked="checked";
				if($ShippingData[$indexClick]['shipping_area'].indexOf($cityGroup[pId][j]['id'])<0)checked='';
				cityList=cityList+"<label class='checkbox-item checkbox-inline'><input type='checkbox' value="+$cityGroup[pId][j]['id']+" "+checked+" data-id="+$cityGroup[pId][j]['id']+">"+$cityGroup[pId][j]['name']+"</label>"   
			}
			$cityList[$cityGroup[pId][j]['id']]=$cityGroup[pId][j]['name'];
		}
		if(empty(cityList))$removeProvinceList+=pId+',';
		content=content+"<section name='"+pId+"' style='display:none' >"+cityList+"</section>";
    }
    content="<div class='alert alert-info' role='alert'>"+content+"</div>";
    $(".cityList").html(content);
    createProvinceList($provinceGroup);
}

```
```
function createProvinceList(data){//构建一级地址checkbox列表
	var ProvinceList='';
	var checked='';
	for(var i=0;i<data.length;i++){
		checked='';
		if($removeProvinceList.indexOf(data[i]['id'])<0){
			if($(".cityList").find("section[name='"+data[i]['id']+"'] input").length==$(".cityList").find("section[name='"+data[i]['id']+"'] input:checked").length){
				checked='checked';
			}
			ProvinceList=ProvinceList+"<div class='checkbox-inline'><input type='checkbox' name="+data[i]['id']+" value="+data[i]['id']+" data-id="+data[i]['id']+" "+checked+">"+"<label class='checkbox-item' data-id="+data[i]['id']+">"+data[i]['name']+"</label></div>" 
		}          
    	}
	if(empty(ProvinceList)){
		ProvinceList="<div class='alert alert-info' role='alert'>所有区域均已选择</div>";
		$ShippingData[$indexClick]='';
		var $this=$("table.traTable").get($indexClick);
		$($this).bootstrapTable("destroy");//摧毁旧行
		$("table.traTable.initTable").removeClass("initTable");//bootstrap删除表格将table标签还原,此时需要去除表格初始化标致，避免后续重复渲染。
		$($this).parents("section").addClass("empty");//摧毁旧行
	}
    else{ProvinceList="<div class='alert alert-info' role='alert'>"+ProvinceList+"</div>";}
	$(".provinceList").html(ProvinceList);
}
```
+ I use Bootstrap-Modal to show my region-selection,click the button above will open the Modal and trigger the hook functions to create the checkboxs, which will removes the checked checkboxs in other lines. The main idea of removing is that All the Children(ajax data $cityGroup) - other lines Chilren($removeCityList) = the Children we need to display.
+ $removeCityList is the string which split by ',' with other lines Children's Id, map the $cityGroup and use indexOf to judge the Children which need to be removed.
+ Based on the principle, do the same job to the Parent.
+ 我使用了Modal模态窗口来呈现地址选择组件，“新增配送区域”将会打开这个模态窗，从而触发模态的钩子函数，执行二级地址checkbox的构建，其中也包括了剔除其他行已出现地址的操作，剔除的主要思想是，所有的二级地址（异步获取的数据$cityGroup）- 非当前区域行的二级地址（$removeCityList） = 需要显示的二级地址。
+ $removeCityList是一个以‘，’分隔符拼接二级地址Id字符串，通过遍历异步获取的数据$cityGroup并借助indexOf来判断每一个二级地址是否剔除
+ 在此基础上，同理构建一级地址。

### 2.checkbox click Listeners 地址点击事件监听

```
function get_city(id){//点击一级地址名称事件，显示所有二级地址
	if(!id > 0){
		return;
	}
	$provinceId=id;
	$(".cityList").find("section").hide();
	$(".cityList").find("section[name='"+$provinceId+"']").show();
	$("#cityName").text($provinceList[$provinceId]);
	$(".cityList").parent().show();
}
function get_city_input(id,e){//点击一级地址checkbox框事件，全部/不全选
	$provinceId=id;
	$(".cityList").find("section").hide();
	$(".cityList").find("section[name='"+$provinceId+"']").show();
	$("#cityName").text($provinceList[$provinceId]);
	$(".cityList").parent().show();
	if($(e).is(':checked')){
		$(".cityList").find("section[name='"+$provinceId+"'] input").prop("checked",true);
	}else{
		$(".cityList").find("section[name='"+$provinceId+"'] input").prop("checked",false);
	}
}
//点击二级地址触发事件,将勾选地址加入$cityGroupSelected
function get_province(cityId,e){
	//window.event.preventDefault();
	window.event.stopPropagation();
	//判断是否全选
	if($(".cityList").find("input").length==$(".cityList").find("input:checked").length){
		$("input[name='"+$provinceId+"']").prop("checked",true);
		//添加全选的一级地址id
	}else{
		$("input[name='"+$provinceId+"']").prop("checked",false);
	}
}
```
+ Children Listener get_city() : show the Children which belong to the Parent when click the Parent's Name
+ Children Listener get_city_input() : check /uncheck the Chilren which belong to the Parent when check /uncheck the Parent
+ Parent Listener get_province() : check /uncheck the Parent when (all its Children has been checked )/(not all its Children has been checked). 

### 1.Init 初始化

```initTra()
	function initTra($data){
		//生成配送表格
		var fragment = document.createDocumentFragment();
		$($data).each(function(i,e){
			var $s = document.createElement("section");
			var $e = document.createElement("table");
			$e.setAttribute('class','traTable initTable');
			$e.setAttribute('name',$index++);
			$s.appendChild($e);
			fragment.appendChild($s);
		});
		$(".traTablelist").append(fragment);
		var $table = $('table.initTable');
		$($data).each(function(i,e){
			var $d=[];
			if(parseInt(e['is_default'])==1){
				$c=[[{
					field: '',
					title: '配送区域',
					align: 'left'
				},{
					field: '',
					title: '默认',
					align: 'right',
					colspan: 3,
				}],[...];
			}else{
				$c=[[{
					field: 'shipping_area',
					title: e.shipping_area_name+'<div class="tool-inline"><span class="label label-primary edit">编辑</span><div style="margin-right:15px"></div><span class="label label-danger delete">删除</span></div>',
					colspan: 4,
				}],[...]];
			}
			$d.push(e);
			var oTraTable = new TraTableInit($table[i],$c,$d);
			oTraTable.Init();
			//初始化表格内的修改&删除按钮事件
			var oTraButtonInit = new TraButtonInit($table[i]);
			oTraButtonInit.Init();
		})
	}
```
+ $data is the data which already exists, I init the Bootstrap-table to show my data，there are 2 kinds of columns setting for Bootstrap-table including 'default' and 'custom'. Avoid changing DOM frequently, it is necessary to use 'createDocumentFragment()'.
+ For better using, X-editable is used by funtion TraButtonInit(). See the screenshot next.
+ $data 是已保存的数据，初始化已存在的数据并用Bootstrap-table显示，同时导入的列表项数据有“默认”与“自定义”2类，为避免插入表格多次操作DOM，此处还使用了createDocumentFragment()，之后再统一操作DOM
+ TraButtonInit（）按钮初始化中还使用了X-editable，来实现a标签点击可修改的效果，如下图所示

![My project demo 5](https://raw.githubusercontent.com/xuzijie1995/Bootstrap-region-selection/master/images/screenshot_6_2.png)

### 2.Init 初始化




to be continue
