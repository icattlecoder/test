     
 <table>
 <thead>
 <tr>
 <td>用户程序</td>
<td>七牛云存储</td>
 </tr>
 </thead>
 <tr> 
 <td>
 
``` javascript
//初始化帐号信息
AccessKey = 'your AccessKey'
SecretKey = 'your SecretKey'
//设置上传策略
PutPolicy.scope = "bucket"
PutPolicy.deadline = 1451491200  //2015-12-31 00:00:00
//PutPolicy.returnUrl = 'http://domain.com'
//PutPolicy.returnBody = base64("body")
//...
//生成token
put_policy = json_encode(PutPolicy)
encoded = base64(put_policy)
signature = hmac_sha1(SecretKey,encoded)
encoded_sign = base64(signature)
upload_token = Accseekey + ":" + encoded_sign + ":" + encoded

post_data['key'] = 'new_key' 
post_data['token'] = upload_token
post_data['file'] = 'your file path'
post_data['x:username'] = 'username'
//multipart/form-data提交表单至七牛
ret = webClient.MultiPost(post_data,"http://up.qiniu.com")

```
 
 </td>
 <td>
 </td>
 <tr>
 <td>
 </td>
 <td>
Response Headers
 
``` 
HTTP/1.1 200 OK
Server: nginx/1.0.14
Date: Thu, 08 Aug 2013 09:38:17 GMT
…
… 
Pragma: no-cache
X-Content-Type-Options: nosniff
X-Log: BDT;BDT;LBD:1;rs.put:85;UP:88
X-Reqid: uT8AAIWMj-2BXxgT
```

Response Body

``` json
{
  "hash":"FltYsrYqyqv3v7Xt6CZL2Xb5ATxT",
  "key":"FltYsrYqyqv3v7Xt6CZL2Xb5ATxT"
}
``` 
 </td>
 </tr>
 <tr>
 <td>

```javascript
if(ret.ok){
	print(ret.hash)
	print(ret.key)
} 
```
 </td>
 
 <td>
 </td>
 </tr>
 
 </table>
