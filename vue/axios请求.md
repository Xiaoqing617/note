# 下载

```
npm install axios
```

# 引入

```js
<script src="/node_modules/axios/dist/axios.js"></script>
```

# 基本使用

```js
<script>
	axios({
		method:'get',  //请求方式
		url:'http://localhost:3000/todo/1',   //请求地址
		data:{ name:'刘晓青',flag:true },    //设置请求的数据（post请求和put请求等数据）
		params:''   //设置请求的参数（get请求和delete）
	}).then(function(tes){//function中如果要用this可以写成tes=>{}
		//处理成功的结果，res是axios给我们封装的一个对象，服务器返回的数据在res.data中
			console.log(res.data)
	}).catch(function(err){//访问失败返回错误操作
				console.log(err)
	})
</script>
```

