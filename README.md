前端JavaScript代码规范 
===

## 符合标准的代码

1. 一个代码段的结束必须以分号结尾

	注: for循环，if条件等大括号外无需分号

2. 避免额外的逗号

	```javascript
	var arr = [1,2,]; // deprecated
	var arr = [1,2]; // 对
	```

3. 为内置构造函数，添加原型时，要进行判断，防止混乱  
	```javascript
	if (typeof Object.property.myMethod !== 'function') {
		Object.prototype.myMethod = function(){
			...
		};
	}
	```

4. for in 循环 必须使用hasOwnProperty 检测，避免来自原型链的污染

	```javascript
	for (var prop in obj) {
	    if (obj.hasOwnProperty(prop){
			// do something
		}
	}
	```

5. 不使用未声明的变量，变量写函数开始

	```javascript
	function getData(value){
		var result;		
		...
		return result;
	}
	```

6. 对象，数组 使用字面量写法

	```javascript
	var obj = {};
	var arr = [1,2];
	```

7. 在非(两者类型不同)的情况下用严格判断 === , !==

8. 循环中 遇到DOM类的操作 用len来存储List的长度，否则每次都会去页面进行获取(性能层面)

9. 一个函数中使用超过两次的变量属性，存储到本地变量中(性能+易读)

	```javascript
	var elemStyle = element.style;
	```

10. 出现回调函数

	我们App中经常会出现回调函数，为防止出错，用self代替想要使用的this


## 命名

1. 驼峰命名法(Camel Case)


2. 构造器,首字母大写

	```javascript
	function Dialog(){
		
	}
	```
	注: 我们项目中的一般为Model，View，Collection 等

3. 常量名全大写 中间用'_'下划线隔开

	```javascript
	var MAX_COUNT = 5;
	```

4. 动名词规范,避免歧义  
	
	这个推敲下统一使用

	**变量名 名词**
	<table>
	  <tr>
	    <th>类型</th><th>示例</th>
	  </tr>
	  <tr>
	    <td>状态</td><td>animated，changed</td>
	  </tr>
	  <tr>
	    <td>迭代</td><td>item，index，el</td>
	  </tr>
	  <tr>
	    <td>引用自身</td><td>self</td>
	  </tr>
  
	</table>
	**函数名 动词**
	<table>
	  <tr>
	    <th>类型</th><th>示例</th>
	  </tr>
	  <tr>
	    <td>设置，读取</td><td>setData,getData</td>
	  </tr>
	  <tr>
	    <td>判断前缀</td><td>options,attrs,params,value(val),obj</td>
	  </tr>
	  <tr>
	  	<td>取消前缀</td><td>dismiss</td>
	  </tr>
	</table>
	** 常用命名 约定**
	<table>
	  <tr>
	    <th>类型</th><th>示例</th>
	  </tr>
	  <tr>
	    <td>对话框</td><td>dialog</td>
	  </tr>
	  <tr>
	    <td>遮盖物</td><td>overlay</td>
	  </tr>
 	  <tr>
	    <td>遮罩</td><td>mask</td>
	  </tr>
	</table>

	需要推敲的部分

	**PS**: 
	1. 如果是要指定某一部分改变，用 部分名+changed 来表示，如headChanged，syncChanged 还是用sync_changed 好  

	2. 事件处理函数命名(事件相应函数): 变化部分 + 动作 如:inputFocus 1，2 都属于事件处理的部分  
	如果是执行某一动作然后触发 toggleToEnablepost 执行这一动作达到什么目的？
	'click #taked-photo': 'photoMenu' 是showPhotoMenu更好？
	togglePostEnabled ，或者仅仅是enablePost()

	3.   形参命名 传数据用？attributes,  选项类的? options，一个对象？obj，还是能代表对象类型的，train
	值类型的 val, value

	4. disableDefaultUI, enableDefaultUI 某些按钮的开启是否可以用这种命名,isPost->enablePost

	5. mode ? (1，2，3，4) 一个功能多种效果？

	6. 迭代用哪一种 item

	7. 字符串型 str, msg(消息)

	8. 模板，tmpl, 如果指定某一特定的模板 userTmpl

	9. 某一个模块 PrivacyWidget 还是 PrivacyView

	**PS**: 函数及流程方面

	1. 对于常用的流程 init->fetchData->render

		解耦？fetchData中对数据做处理否？

	**PS**: 如何写一个模块  

	以前App.Views.Default = Backbone.View.extend();

	优化: 
	```javascript
	var DefaultView = Backbone.View.extend({});
	return DefaultView;

	return Backbone.View.extend({

	});
	```


5. 约定俗称
action，dismiss(取消)，addOne, addAll，loadMore，tmpl，build(哪里用)

## 代码格式化
1. tab还是空格  
	一般tab代表4个空格，如无特殊说明，下面一个tab都代表4个空格

2. 注释  
	* “//” 单行注释 注释内容与标致留一个空格
	* “/* */” 多行注释，可以用在某些特殊情况，如参数注释
	* 对一个函数或者一段代码的注释写上面 用
	* 对一行代码 中某个变量注释 写右边
	注 尽可能用变量名，函数名能代表你的意图，而用注释来说明你代码为何这样写，是要处理什么问题


3. 多个var声明 下一行用tab隔开，非赋值写第一行，赋值的都统一写一行

	```javascript
	var result, difference,
		self = this,
		mathFloor = Math.floor;
	```

4. 折行,如果代码过长要进行折行处理 这里用两个tab更加清晰	

	```javascript
	// 函数调用，两个tab比较舒服，链式调用一个tab就可
	callAFunction(document, element, window, 'some string value', true, 123,
			navigator);
	// 判断: 两个tab
	if (isLeapYear && isFebruary && day == 29 && itsYourBirthday &&
			noPlans) {
		// do something
	}
	// 字符串连接 内容对齐
	var longString = "Here's the story, of man " +
					 "nam Brandy";
	```

5. switch 模式  
	
	var inspect_me = 0,
		result = '';
	switch (inspect_me) {
		case 0:
			result = 'zero';
			break;
		case 1:
			result = 'one';
			break;
		default: 
			result = 'unkonw';
	}

	**PS:** 还是case对齐 switch

6. 模块书写格式

**希望作为引子**
* 常用判断简写，判断优化
* 经常出现的问题，可以作为一个FAQ库，供查询
* 常见问题的解决方案，即模式

<!-- 
    var Schema = mongoose.Schema
      , ObjectId = Schema.ObjectId;

    var BlogPost = new Schema({
        author    : ObjectId
      , title     : String
      , body      : String
      , date      : Date
    });

```javascript
case 1:
	// do something
	break;  

case 2:
	// do something
	break;
``` 


-->