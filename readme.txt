AJAX 异步的JavaScript和XML
异步 局部更新网页
XMLHttpRequest（XHR）对象 与web服务器实现异步
var request;
if (window.XMLHttpRequest) {
	request = new XMLHttpRequest();//IE7+,Firefox,Chrome,Opera,Safari...
} else {
	request = new ActiveObject("Microsoft.XMLHTTP");//IE6,IE5
}

HTTP 一种无状态协议
请求方式
GET:
一般用于信息获取；使用url传递参数；对所发送信息的数量有限，一般在2000个字符
POST:
一般用于修改服务器上的资源；对所发送信息的数量无限制

HTML状态码：
1××：信息类，表示收到web浏览器请求，正在进一步处理中
2××：成功，用户请求被正确接收，eg：200
3××：重定向，请求失败，客户需采取进一步动作
4××：客户端错误，表示客户端提交的请求有错误，eg：404
5××：服务器错误，表示服务器不能完成对请求的处理 eg：500

XHR对象 方法
open(method,url,async);
send(string);

GET请求：
request.open("GET","get.php",true);
request.send();

POST请求：
request.open("POST","set.php",true);
request.setRequestHeader("Content-type","application/x-www-form-urlencoded");
request.send("name=figer&sex=female");

XHR取得响应

readyState属性
0：请求未初始化
1：服务器连接建立，open已调用
2：请求已接收，接收到头信息
3：请求处理中，接收到响应主体
4：请求已完成，响应完成

responseText 获得字符串形式的响应数据
responseXML  获得XML形式的响应数据
status和statusText 以数字和文本形式返回HTTP状态码
getAllResponseHeader() 获取所有响应报头
getResponseHeader() 查询响应中某个字段的值


var request = new XMLHttpRequest();
request.open("GET","get.php",true);
request.send();
request.onreadystatechange = function() {
	if(request.readyState === 4 && request.status === 200) {
		//do something request.responseText
	}
}

===========================================================================
PHP:创建动态交互性站点的服务器端脚本语言

作用：
能够生成动态页面内容
能够创建、打开、读取、写入、删除以及关闭服务器上的文件
能够接受表单数据
能够发送并取回cookies
能够添加、删除、修改数据库中的数据
能够限制用户访问网站中的某些页面

运行php:
web服务器
软件包XAMPP https://www.apachefriends.org/download.html

===========================================================================
JSON：js对象表示法

是存储和交换文本信息的语法，类似XML
独立于语言，不管什么语言，都可以解析json
长度短小
读写速度快
可以使用js内建的方法直接进行解析，转换成js对象

解析
var jsondata = '{
	"staff":[
		{
			"name":"洪七",
			"age":70
		},
		{
			"name":"郭靖",
			"age":35
		},
		{
			"name":"黄蓉",
			"age":30
		}
	]
}';

var jsonobj = eval( '(' + jsondata + ')' );
或 var jsonobj = JSON.parse(jsondata);

JSONLint json在线校验

======================================================
跨域
http://    www    .   abc.com   :   8080    /   scripts/jquery.js
协议       子域名     主域名        端口号      请求资源地址

协议、子域名、主域名、端口号中任意一个不同时，都算跨域

解决跨域：
1.后台代理
2.JSONP 只能处理get请求的跨域 

前端
dataType: "jsonp",//jsonp
jsonp: "callback",//callback与后台一致

后端
$jsonp = $_GET["callback"];//callback与前端保持一致
echo $jsonp . '({"success":false,"msg":"参数错误"})';

3.XHR2 (XMLHttpRequest level2 ,IE10以下版本不支持)
后端
header("Access-Control-Allow-Origin:*"); 
header("Access-Control-Allow-Methods:POST,GET"); 


