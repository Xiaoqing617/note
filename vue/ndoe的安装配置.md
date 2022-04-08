https://blog.csdn.net/lpq3621/article/details/116614087

**一、Node.js的安装**

直接官网下载安装，安装位置是自定义文件夹（记得最后一个框不要点）

我的安装位置是D:\zidingyianzhaung\nodejs

**二、安装测试**

打开命令行输入node -v，然后回车会显示版本号，例如：v16.14.2

输入npm -v，回车也会有个版本号，例如：8.5.0

**三、路径修改**

在自己的安装目录下创建两个文件夹node_global和node_cache

然乎打开命令行输入npm config set prefix "自己的安装目录\node_global"    例如我的就是npm config set prefix "D:\zidingyianzhaung\nodejs\node_global"    然后回车

再次输入一行命令npm config set cache "自己的安装目录\node_cache"   例如：npm config set cache "D:\zidingyianzhaung\nodejs\node_cache"

**四、环境变量的配置**

右击此电脑点击高级设置点击环境变量，

在系统变量中添加变量，变量名为NODE_PATH，变量值为  自己的安装目录\node_modules，例如我的就是    D:\zidingyianzhaung\nodejs\node_modules

在用户变量的PATH中将默认的 `C` 盘下 APPData/Roaming\npm 修改为 D:\zidingyianzhaung\nodejs\node_global

**五、下载测试**

打开命令行（注意一定是用管理员身份打开的）输入npm install webpack -g   等运行结束之后去自己创建的那两个文件夹中看看有没有内容，有内容说明成功了

如果失败了，就在命令行中输入npm config list 查看以下两行代码，如果有一个或者两个是在C盘中则重新去进行第三步（注意：哪个是C盘就进行哪个，另一个配置好的不需要动）

cache = "D:\\zidingyianzhaung\\nodejs\\node_cache"
prefix = "D:\\zidingyianzhaung\\nodejs\\node_global"