     
 <table> 
   <tr> 
  <td rowspan="2" >
 		
 ** 应用客户端(APPClient) **
 
 
 
``` java
/*********************************
*           SETP 1
* 向服务端请求上传token
* 
**********************************/
upload_token = AppServer.GetToken();



/************************************
*			SETP3
*从服务端接收到上传的token后，将文件上传至七牛
*
*************************************/
		
ret = IOClient.PutFile(upload_token,
		file_path,
		key,
		putExtra);

				
				
				
/************************************
*		SETP 7
* 七牛回调成功后，将回调服务器返回给七牛的数据
* 原封不对的返回给客端，客户端对其json反序列化
*
*************************************/

				
				
result = JsonDecode(ret.responseText);
print(result.filename);
print(result.uid);
print(result.msg);

```

</td>
<td colspan=2>
** 服务端(APPServer)  **

``` php
/**************************************
*			SETP 2
* 服务端使用sdk,生成upload token,颁发给应用客户端
* 在这个上传模型中，我们指定上传的回调地址以及回调内容
*
**************************************/

public GetToken(){
	$AccessKey = "your accessKey";
	$SecreteKey = "your secreteKey"
	$putPolicy = new Qiniu_RS_PutPolicy($bucket); 	
	//指定上传成功后，由七牛服务向指定的Url服务器POST数据
	//数据内容由callbackBody指定
	$putPolicy->callbackUrl = "http://requestb.in/1jv3ef41";
	$putPolicy->callbackBody='name=$(fname)}&uid='.session('uid');
	$upToken = $putPolicy->Token(null); 
	echo $upToken;
}
```

</td>
</tr>
<tr>
<td>
** 七牛云存储 **

```
/**************************
*		SETP4
* 成功接收上传的文件后post
* callbackBody到callbackUrl
* 
***************************/
…
```

```
/*******************************
*			SETP 6
* 从回调服务器接收到状态码为200的响应后，
* 向客户端返回以下数据包
*
******************************/

//Response Headers 

HTTP/1.1 200 OK
…
X-Log: BDT;BDT;LBD:1;rs.put:7;UP:11/301
X-Reqid: -BIAAKA3FfObmBkT

//response Body

{
 "filename":"hello-qiniu.txt",
 "uid":"123",
 "msg":"ok"
}
```


</td>
<td>
** 回调服务器(CallBack Server)  **

``` php
/*********************************
*			SETP 5
* 回调服务器，接收七牛POST过来的数据,
* POST DATA,形如:uid=123&name=hello-qiniu.txt
* 最后需要返回七牛状态码200,body为json格式的回应
************************************/

public ResponeQiniu(){
	$data["filename"] = $_POST["name"];
	$data["uid"] =$_POST["uid"];
	$data["msg"] = "OK";
	$uid = $_POST["uid"];
	echo $json_encode($data);
}
```


</td>
</tr >
</table>
