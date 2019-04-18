
#### 简介
	
inkage 是一款原生开源的 javascript 插件，用于生成省市区选择器，基本用法十分简单。<br>
注意：test.js为最初测试版本 具体以inkage.js为准<br>
[预览](https://ginobili20.github.io/inkage/)


#### 原理
利用了select的onchange事件，省份的onchange事件，触发市的onchange事件，市的onchange事件确定区的选择范围，从而形成了三级联动，<br>
自定义属性prov_index存放数组下标，获取相应的市数组，然后根据市数组以及city_index获取区数组
```
this.province.options[this.province.selectedIndex].getAttribute('prov_index')
```

#### 使用方法

最简单的使用只需要两个步骤：

1. 放置容器，引入依赖

		<!--存放省市区数据的三个 select-->
		<select id="province"></select>
		<select id="city"></select>
		<select id="district"></select>
		
		<!--引入插件-->
		<script src="./inkage.js"></script>

2. 调用方法
```
     var inkage = new Inkage({
        provinceId: 'province',
        cityId: 'city',
        districtId: 'district'
    })
```

#### API
目前只设计了一个api <br>
方便获取表单值  <br>
可以接受参数，当然也有默认参数 例如
 ```
  document.getElementById('getValue').onclick = function () {
        var val = inkage.getValue('|')
        console.log(val)
    }
 ```
 指定拼接成一定格式的字符串进行返回,以|为例(当然也可以使用其他字符串)
 返回如下：
	
		"广东省|广州市|越秀区"


#### 插件的编写
一个可复用的插件需要满足以下条件：

插件自身的作用域与用户当前的作用域相互独立，也就是插件内部的私有变量不能影响使用者的环境变量；<br>
插件需具备默认设置参数；<br>
插件除了具备已实现的基本功能外，需提供部分API，使用者可以通过该API修改插件功能的默认参数，从而实现用户自定义插件效果；<br>
插件支持链式调用；<br>
插件需提供监听入口，及针对指定元素进行监听，使得该元素与插件响应达到插件效果。<br>

插件的几种写法：<br>
1.面向对象的方式 （这里使用的是这种方式） 
```
//自定义类    
function plugin(){}

//提供默认参数
plugin.prototype.str = "default param";

//提供方法(如果不传参,则使用默认参数)
plugin.prototype.firstFunc = function(str = this.str){
    alert(str);
}

//创建"对象"
var p = new plugin();
//调用方法
p.firstFunc("Hello ! I am firstFunc");//Hello ! I am firstFunc
p.firstFunc();//default param
```

2.闭包
```
var plugin =(function(){
    function _firstFunc(str){
        alert(str);
    };
    return{
        firstFunc: _firstFunc,
    };
})();
```

#### 补充
在定义插件之前添加一个分号，可以解决js合并时可能会产生的错误问题；<br>
undefined在老一辈的浏览器是不被支持的，直接使用会报错，js框架要考虑到兼容性，因此增加一个形参undefined，就算有人把外面的 undefined 定义了，里面的 undefined 依然不受影响；<br>

[参考](https://www.jianshu.com/p/e65c246beac1)
