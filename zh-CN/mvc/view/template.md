---
name: 模板函数
sort: 2
---

# 模板函数

beego 支持用户定义模板函数，但是必须在 `beego.Run()` 调用之前，设置如下：

	func hello(in string)(out string){
		out = in + "world"
		return
	}
	
	beego.AddFuncMap("hi",hello)

定义之后你就可以在模板中这样使用了：

	{{.Content | hi}}

目前 beego 内置的模板函数如下所示：

* dateformat

	实现了时间的格式化，返回字符串，使用方法 {{dateformat .Time "2006-01-02T15:04:05Z07:00"}}。

* date

	实现了类似 PHP 的 date 函数，可以很方便的根据字符串返回时间，使用方法 {{date .T "Y-m-d H:i:s"}}。

* compare

	实现了比较两个对象的比较，如果相同返回 true，否者 false，使用方法 {{compare .A .B}}。

* substr

	实现了字符串的截取，支持中文截取的完美截取，使用方法 {{substr .Str 0 30}}。

* html2str

	实现了把 html 转化为字符串，剔除一些 script、css 之类的元素，返回纯文本信息，使用方法 {{html2str .Htmlinfo}}。

* str2html

	实现了把相应的字符串当作 HTML 来输出，不转义，使用方法 {{str2html .Strhtml}}。

* htmlquote

	实现了基本的 html 字符转义，使用方法 {{htmlquote .quote}}。

* htmlunquote

	实现了基本的反转移字符，使用方法 {{htmlunquote .unquote}}。

* renderform

	根据 StructTag 直接生成对应的表单，使用方法 {{&struct | renderform}}。