街旁代码规范 
===

这是一份街旁的代码规范

## 符合标准的代码

1. 必须以分号结尾(有例外)

2. 避免额外的逗号
```javascript
var arr = [1,2,]; // 错
var arr = [1,2]; // 对
```

3. 这是第三个项目
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

## 命名

这个是命名规范

>1. 驼峰命名法(Camel Case)


>2. 构造器,首字母大写
```javascript
function Dialog(){
	...
}
```
>3. 常量名全大写 中间用'_'下划线隔开
```javascript
var MAX_COUNT = 5;
```

>4. 动名词规范,避免歧义  
>*变量名 名词*
<table>
  <tr>
    <th>ID</th><th>类型</th><th>示例</th>
  </tr>
  <tr>
    <td>1</td><td>状态</td><td>animated,changed</td>
  </tr>
  <tr>
    <td>2</td><td>迭代</td><td>item,index</td>
  </tr>
</table>
>*函数名 动词*
<table>
  <tr>
    <th>ID</th><th>类型</th><th>示例</th>
  </tr>
  <tr>
    <td>1</td><td>设置，读取</td><td>setData,getData</td>
  </tr>
  <tr>
    <td>2</td><td>判断前缀</td><td>options,attrs,params,value(val),obj</td>
  </tr>
</table>

>5. 约定俗称
action

## 代码格式化
1. tab还是空格  
>一般tab代表4个空格，如无特殊说明，下面一个tab都代表4个空格

2. 注释  
>* “//” 单行注释 注释内容与标致留一个空格
>* “/* */” 多行注释，可以用在某些特殊情况，如参数注释
>* 对一个函数或者一段代码的注释写上面 用
>* 对一行代码 中某个变量注释 写右边
>注 尽可能用变量名，函数名能代表你的意图，而用注释来说明你代码为何这样写，是要处理什么问题

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

5. 空行的使用，应该向写文章一样段落化，一个段落一个小功能，不过这个因人而异，也许上下对齐的更适合你
```javascript
if (wl && wl.length) {

	for (var i = 0, l = wl.length; i < l ; i++) {
		p = wl[i];
		type = Y.lang.type( r[p] );

		if (s.hasOwnProperty(p)) {

			if (merge && type == 'object') {
				Y.mix( r[p], s[p] );
			} else if (ov || !(p in r)) {
				r[p] = s[p];
			}
		}
	}
}
```

6. switch 每个case之间一个空行
```javascript
case 1:
	// do something
	break;  
>
case 2:
	// do something
	break;
```

*希望作为引子*
* 常用判断简写，判断优化
* 经常出现的问题，可以作为一个FAQ库，供查询
* 常见问题的解决方案，即模式