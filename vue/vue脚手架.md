vue CLI

# 安装

```js
npm install -g @vue/cli
vue --version//检查版本是否正确
```

# 创建一个项目

```js
vue create 项目名 //想在哪创建就在哪个文件夹中运行这个命令
//也可以使用可视化工具去创建，在文件夹中输入vue ui会打开一个可视化网页
```

然后选择自己需要的东西

当有需要自己配置在webpack.config.js中的配置时，可以创建vue.config.js文件，比如起服务的时候想要自己修改端口可以在文件中写入：

```js
module.exports={
  devServer:{
    port:3000,//自己想要的端口号
    open:true//起服务后是否自己打开网页
  }
}
```

