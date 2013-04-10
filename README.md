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
			// do something
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
		// do something
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


11. 警惕浅复制

	浅复制很容易出错

	
## 命名

1. 驼峰命名法(Camel Case)


2. 构造器,首字母大写

	```javascript
	function Dialog(){
		// do something
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
	    <td>判断前缀</td><td>can,is,has</td>
	  </tr>
	  <tr>
	  	<td>取消前缀</td><td>dismiss</td>
	  </tr>
	  <tr>
	  	<td>开启</td><td>enable</td>
	  </tr>
	  <tr>
	  	<td>关闭</td><td>disable</td>
	  </tr>
	</table>
	**常用命名 约定**
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
	
5. 约定俗称
常用: action，dismiss(取消)，addOne, addAll，loadMore，tmpl，build

* 状态改变: 块名+changed 如:syncChanged
* 事件响应函数: enableButton，函数名仅来代表函数要执行的操作  
	特例：togglePostState 即点击会根据情况做不同操作  
  	函数名最好能代表要进行的操作 showPhotoMenu	
* 形参 attributes 或 options  
  当要传递的某一个数据的一些属性时 ->attributes  
  当要传递**设置** 时 ->options
* View or Widget  
	可复用性的View用Widget后缀  
	单次用的View用View后缀


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

5. switch 模式  switch，case 对齐
	```javascript
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
	```
	

6. 模块书写格式

	```javascript
	// 代码较多，文件中可能包含一帮助函数
	var DefaultView = Backbone.View.extend({
		...
	});
	return DefaultView;

	// 代码短小的情况下
	return Backbone.View.extend({

	});
	```

7. 执行流程 render
	
	```javascript
	// 任务交给fetchData执行
	render: function(){
		this.fetchData();
		return this;
	},

	fetchData: function() {
		var self = this;
		App.Helpers.api(this.api.url, this.api.data, function(r){
			handleData(r); // 若handleData 代码量较少，可以不提
		});

		function handleData(results) {
			self.collection.add(results.likes);
            if (self.api.data.page == 1) {
                Crab.setTitle({
                    title: String(results.total)
                });
            };
            if(results.has_more) {
                self.$el.append(self.loadMoreWidget.render().el);
            } else {
                self.loadMoreWidget.destroy();
            }
		}
	}
	```


注: 6,7 可以独立出来，作为专有的 项目代码 格式

**希望作为引子**
* 常用判断简写，判断优化
* 经常出现的问题，可以作为一个FAQ库，供查询
* 常见问题的解决方案，即模式


**项目待解决**
* 复用问题，如何优雅的实现，并且非常容易找 模块的复用，代码的复用


一些命名空间的使用，如
this.api.
防止存储数据时冲突
this.data.venue = 
this.data.venueList = 