扩展Javascript编程规范
=== 

参考对象: [google Javascript编程规范]()  
		[javascript 编程规范 司徒正美](http://www.cnblogs.com/rubylouvre/archive/2011/04/02/2003151.html)

1. 若想调用函数自身，禁止使用命名函数表达式，在目标函数的第一行编写一下代码实现，详解请google 《命名函数表达式揭秘》：  
	```javascript
		var self = arguments.callee;
	```

2. 注释 JSDoc ？


3. 禁止快内函数声明  
	```javascript
		if (x) { // ng no good
			function foo(){};
		}
	```

4. 标准特性优于非标准特性（如果类库有提供，优先使用类库中的函数）  
	```javascript
		$("XXXX").find("YYYY").find("ZZZZ"); //ng
		$("XXXX").next() //或者nextUntil, nextAll, prev, prevAll, prevUntl, children, closest, siblings
	```

5. 为元素添加事件时，考虑的顺序是delegate > live > bind

6. 命名空间的使用 (作为参考和学习)
	```javascript
	;;;$(function(){
	//...其他用到的变量
	        var $$ = window.$$ = {
	          //本页面私有的辅助函数1
	          _assist1:function(){
	 
	          },
	          //本页面私有的辅助函数2
	          _assist2:function(){
	 
	          },
	          //本页面私有的辅助函数3
	          _assist3:function(){
	 
	          },
	          //本页面私有的辅助函数4
	          _assist4:function(){
	 
	          },
	          //本页面私有的辅助函数5
	          _assist5:function(){
	 
	          },
	//....更多的私有函数
	          //功能1
	          feature1:function(){
	 
	          },
	          //功能2
	          feature2:function(){
	 
	          },
	          //功能3
	          feature3:function(){
	 
	          },
	          //功能4
	          feature4:function(){
	 
	          },
	          //功能5
	          feature5:function(){
	 
	          },
	          //从后台获取的JSON数据统一放到这个对象中，以便其他函数调用
	          jsons:{},
	//....更多需求，一个需求对应一个函数
	          main:function(){
	            $$.feature1();
	            $$.feature2();
	            $$.feature3();
	            $$.feature4();
	//....在main主函数中调用它们。
	          }
	        }
	        $$.main();
	      });
	```

7. 函数声明 函数表达式
	```javascript
		function foo(){} // 声明
		var foo = function(){}; // 函数表达式 作为赋值函数的一部分  
		new function bar(){}; // 表达式 是new表达式  
	```
() 括号 是一个分组操作符，内部只能包含表达式  
JSON 字符串 常包含在一个圆括号内: eval( '('+JSON+')' ); 这样做就是为了分组操作符，也就是这对括号，会让解析器强制将JSON的花括号解析成表达式而不是代码块。

函数声明会在任何表达式被解析和求值之前先被解析和求值

8. 命名函数表达式
	```javascript
		 var f = function foo(){
		    return typeof foo; // foo是在内部作用域内有效
		  };
		  // foo在外部用于是不可见的
		  typeof foo; // "undefined"
		  f(); // "function"
	 ```

	 var f = function foo(){} 就是命名函数表达式  
	 给它一个名字就是可以让调试过程更方便，

9. 