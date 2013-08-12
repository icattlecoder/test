     
 <table> 
 	<tr> 
 		<th rowspan="2" >
 ** 应用客户端(APPClient) **
 
``` javascript
//向服务端请求上传token
upload_token = AppServer.GetToken();//=======1====>








//从服务端接收到上传的token后，将文件上传至七牛
ret = IOClient.PutFile(upload_token,
						file_path,
						key,
						putExtra);//--\|/|=3===>



```
</th>
<td>
** 服务端(APPServer)  **

``` php
//服务端使用sdk,生成upload token,颁发给应用客户端
public GetToken(){
	$AccessKey = "your accessKey";
	$SecreteKey = "your secreteKey"
	$putPolicy = new Qiniu_RS_PutPolicy($bucket);
	$upToken = $putPolicy->Token(null); 
	echo $upToken;	
}
//<===2===

```

</td>
</tr>
<tr>
<td>
** 七牛云存储 **

Response Headers
 
``` 
HTTP/1.1 200 OK
Server: nginx/1.0.14
Date: Thu, 08 Aug 2013 09:38:17 GMT
…

```

Response Body

``` 
{
  "hash":"FltYsrYqyqv3v7Xt6CZL2Xb5ATxT",
  "key":"FltYsrYqyqv3v7Xt6CZL2Xb5ATxT"
}
``` 
<======4=======

</td>
</tr>
<tr>
</tr>
</table>
