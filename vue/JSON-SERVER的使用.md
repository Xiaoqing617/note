作用：在不到30秒的时间内获得零编码的完整虚假REST API

# 全局安装

命令行中（注意：用管理员身份打开的）执行npm install -g json-server

当出现类似added 175 packages in 11s这种字样的时候表示成功

# 提供一个json文件

```json
{
    "todo":[
        {"id":1,"name":"温正","flag":true},
        {"id":2,"name":"吃饭","flag":false},
        {"id":3,"name":"睡觉","flag":true},
        {"id":4,"name":"打江森","flag":false}
    ]
}
```

# 启动接口服务

终端执行json-server todo.json

# 特点

JSON-server给我们生成的一个rest风格的接口

```
查询：get    http://localhost:3000/todo   获取所有的任务
			http://localhost:3000/todo/3   获取id为3的任务
增加：post   http://localhost:3000/todo   增加
删除：delete  http://localhost:3000/todo/3  删除id为3的任务
修改：put    http://localhost:3000/todo/3    全量的修改，会把原来的所有值覆盖掉
      patch：打补丁，只会修改传递的值
```

