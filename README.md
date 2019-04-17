#### 简介
	
inkage 是一款原生开源的 javascript 插件，用于生成省市区选择器，基本用法十分简单。<br>
注意：test.js为最初测试版本 具体以inkage.js为准

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
     效果如下

	[界面](https://ginobili20.github.io/inkage/)

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

