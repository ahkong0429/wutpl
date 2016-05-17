
# wu.tmpl.js
极简高性能模板引擎


![性能测试](test/test.png)  
<!-- [性能测试](https://wusfen.github.io/wu.tmpl.js/test/template_test.html) -->


------------------------------------------
## 特性
  * 简单高效
  * 支持初始自动渲染
  * 支持简洁语法({{ }})和原生语法(<% %>)，可同时使用
  * 模板可直接写在目标位置，无需 script 标签或字符串保存模板。也支持这两种方式
  * 支持传参，模板内支持访问全局变量
  * 有进行缓存、传参转为内部变量（不用 with）、过滤频繁更新dom的中间状态等方式优化性能
  * 体积小， 仅 2k 多


------------------------------------------
## 如何使用

1 . 引入 `<script src="path/to/wu.tmpl.js"></script>`。 下载压缩版 [wu.tmpl.min.js](https://cdn.rawgit.com/wusfen/wu.tmpl.js/master/wu.tmpl.min.js)
```html
<!DOCTYPE html>
<html>
<head>
	<!-- 引入 wu.tmpl.js ， 建议放头部，避免闪烁。文件比较小 -->
	<script src="../wu.tmpl.min.js"></script>
</head>
<body>

</body>
</html>
```

2 . 声明模板 `wu-tmpl="options"`
 
`options.render` 是否在页面准备完成时 **自动渲染** 
```html
<!DOCTYPE html>
<html>
<head>
    <title>hello world</title>
    <script src="../wu.tmpl.min.js"></script>
</head>
<body>
    <div wu-tmpl="{render:true}">
        hello {{ 'world' }} !
    </div>
</body>
</html>
```

`options.name`   模板名
```html
<!DOCTYPE html>
<html>
<head>
	<script src="../wu.tmpl.min.js"></script>
</head>
<body>

	<div wu-tmpl="{name:'time'}">
		<% var d = new Date %>

		{{ d.getHours() }}:{{ d.getMinutes() }}:{{ d.getSeconds() }}

		<small> {{ ('00'+d.getMilliseconds()).slice(-3) }} </small>
	</div>

	<script>
		setInterval(function () {
			wu.tmpl.render('time');
		}, 41.666667)
	</script>

</body>
</html>
```

`options.data`   模板数据
```html
<!DOCTYPE html>
<html>
<body>
	<ul wu-tmpl="{name:'list', data:data, render:true}">
		{{each list item i}}
		<li>
			{{ item.name }}
		</li>		
		{{/each}}
	</ul>

	<script>
		var data = {
			list:[
				{id:1, name:'Tom'},
				{id:2, name:'Lily'},
				{id:3, name:'Mary'}
			]
		}
	</script>

	<script src="../wu.tmpl.js"></script>
</body>
</html>
```

3 . 再渲染 `wu.tmpl.render(name, data)`
```javascript
@param  {} name          如果不传，则更新所有模板
@param  {String} name    'data' 
@param  {Object} name    data
@param  {Element} name   element

@param  {Object} data   data of tmpl.  可选
```
```javascript
wu.tmpl.render('data')

// or
wu.tmpl.render(data)

// or
var tpl = documents.getElementById('tplId')
wu.tmpl.render(tpl)
```


------------------------------------------
## 模板语法

### 简洁语法
* if, else, else if
```javascript
{{if 条件1}}
 ...
{{else if 条件2}}
 ...
{{else}}
 ...
{{/if}}
```
* each
```javascript
{{each array item index}}
 ...
{{/each}}
```
* {{ 表达式 }}
```javascript
{{ value }}
```

### 原生语法
* `<% ... %>` 可以写任何原生 js，如：  
```html
<ul>
 <% for(var i = 0; i < 100; i++){ %>
 <li>...<li>
 <% } %>
</ul>
```

* `<%= ... %>` 插入表达式，如：
```html
<p> hello <%= 'world' %> ! </p>
```


------------------------------------------
## 例子

查看源代码，看怎么使用

* [hello world](https://cdn.rawgit.com/wusfen/wu.tmpl.js/master/examples/helloWorld.html) | [源码](examples/helloWorld.html)
* [时钟](https://cdn.rawgit.com/wusfen/wu.tmpl.js/master/examples/time.html) | [源码](examples/time.html)
* [ajax](https://cdn.rawgit.com/wusfen/wu.tmpl.js/master/examples/ajax.html) | [源码](examples/ajax.html)
* [动画](https://cdn.rawgit.com/wusfen/wu.tmpl.js/master/examples/animate.html) | [源码](examples/animate.html)
* [list](https://cdn.rawgit.com/wusfen/wu.tmpl.js/master/examples/list.html) | [源码](examples/list.html)
