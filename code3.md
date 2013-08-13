     
 <table> 
 	<tr> 
 		<td rowspan="2" >
 		
 ** 应用客户端(APPClient) **
 
 
 
``` java
//向服务端请求上传token
upload_token = AppServer.GetToken();//=======1====>








//从服务端接收到上传的token后，将文件上传至七牛
ret = IOClient.PutFile(upload_token,
		file_path,
		key,
		putExtra);//===3===>
		
		
		
		
		
		
		
		
		
		
//=========5=========
//从七牛接收到重定向http包，自动重定向
IOClient.redirect("http://requestb.in/1jv3ef41"+
	"?upload_ret=eyJrZSI6MTIzfQ==")



```

</td>
<td>
** 服务端(APPServer)  **

``` php
//服务端使用sdk,生成upload token,颁发给应用客户端
public GetToken(){
$AccessKey = "your accessKey";
$SecreteKey = "your secreteKey"
$putPolicy = new Qiniu_RS_PutPolicy($bucket);
//指定上传成功后，客户端重定向页面
$putPolicy->returnUrl = "http://requestb.in/1jv3ef41";
$putPolicy->returnBody='{"name":$(fname)}';
$upToken = $putPolicy->Token(null); 
echo $upToken;
//<===2===
}
```

</td>
</tr>
<tr>
<td>
** 七牛云存储 **

Response Headers
 
```
HTTP/1.1 301 Moved Permanently
Server: nginx/1.0.8\r\n
Date: Thu, 08 Aug 2013 09:38:17 GMT
Content-Type: text/plain; charset=utf-8\r\n
… 
Location: http://requestb.in/1jv3ef41?upload_ret=eyJrZSI6MTIzfQ==
…
Pragram: no-cache
X-Log: BDT;BDT;LBD:1;rs.put:7;UP:11/301
X-Reqid: -BIAAKA3FfObmBkT
```
<======4=======

</td>
<tr >
<tr>
<td colspan=2>

** 重定向服务器(APPServer)  **

``` php
//=========6=========>
//重定向服务器，接收returnBody的内容
public GetRetunrBody(){
	$retBody = $_GET["upload_ret"];
	//retBody是经过base64编码，需要解码
	$retBody = Base64Decode($retBody);
	//对解码后的内容进行json反序列化
	$res = json_decode($retBody);
	print_r($res["name"]);
}
```


</td>

</tr>
</table>
