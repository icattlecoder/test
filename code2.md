     
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

//向服务端请求上传token
upload_token = Get();

//使用sdk进行上传
ret = IOClient.PutFile(upload_token,file_path,key,putExtra);

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
