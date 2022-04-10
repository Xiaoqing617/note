# vue笔记

过滤数组this.list=this.list.filter(item => item.id !== id)只把id不同的留下

数组名.some(item=>item.布尔值)只要有一个布尔值是true就返回true

数组名.every(item=>item.布尔值)全部的布尔值是true就返回true

数组名.forEach() 方法对数组的每个元素执行一次提供的函数。



# vue的基本使用：

```vue
<body>
    <div id="app">
        <h1>{{msg}}</h1>    <!--输出hello vue  {{}}在vue中叫插值表达式，可以在视图中展示data的数据，使用的数据必在data中存在，不能写js语句、if、for之类的，可以写表达式。还有只能显示在标签的内容里面，不能用在标签的属性中-->
    </div>
    <script src="vue.js"></script>
    <script>
        const vm=new new Vue({
            el:'#app',         //element的缩写，指定vue管理的视图，某个盒子的选择器，不能指定html和body
            data:{              //指定vue中使用的数据，也可以是对象的形式
                msg:'hello vue',
			   car:{name:'hbh',age:'19'}
            }
	    	computed: { //计算属性
				reverseMsg : function() { return this.msg.split('').reversre().join('') } //这个是计算属性，是写在computed中的，和data属性一样也是属性，属性值是return中的返回值，计算属性中写的是一个函数
				reverseMsg : { //计算属性的完整形式
					get(){ return this.msg.split('').reversre().join('') }
					set(value){ }
	    		}//计算属性默认只有get，默认不能修改计算的值，如果想要修改值需要自己加上一个set，value是拿到的计算值
      		}
	    	watch:{//侦听器
				mag: function(newValue,oldValue){ 函数体 }//侦听简单类型mag是否改变，改变了就执行函数体，参数1新值和参数2旧值
				car: {
					deep:true,//深度监听，监听复杂类型必写的参数，逼近监听地址变化数据变化也会监听
					immediate:true,//立即监听，页面一加载handler函数体就会执行一次
					handler:funtion(value){ 函数体 }//数据变化时执行的函数
				}
	    	}
	    	methods: { delTodo(id){ 函数体 } }     //指定vue中使用到的方法，里面的所有方法中的this都指向vm
        	filter: {demo1:function(value){return value.tpUppereCase()}}//局部过滤器，demo是名字
        	component: { hello:{template:'<div>你好啊</div>'}}//局部组件
        })
        Vue.filter('demo',funtion(value){  //全局过滤器的定义，经常用于格式化文本、时间(可以引入moment.js)以及数字，demo是过滤器的命名，value是接收到的待处理数据，过滤器的使用是在插值表达式中例如{{msg|demo|demo1}},也可以在v-bind中使用例如v-bind:id="msg|demo"。过滤器可以接受参数如{{msg|demo(i,j)}}这样我们的参数就会有三个
               return  value.toUpperCase()  //将数据变为大写并返回
         })
         Vue.component('hhh',{//组件，hhh是组件名，组件当成标签使用<hhh></hhh>
           template:`
			<div>你好啊<button>按钮</button></div>
			`,
           data:function(){
             return {money:1000,car:'玛莎拉蒂'}
           }
           router:router//关联路由对象，冒号后面的router是路由对象的名字
         })
    </script>
</body>
```

# 路由的基本使用

1. 下载vue-router:npm install vue-router@3
2. 引入vue-router（必须在vue.js后面引入）
3. 创建路由对象，路由对象就是用来管理路由的：const 路由对象名字=new VueRouter()
4. 关联vue实例和路由对象，在vue实例中添加参数router:路由对象名字
5. 给路由对象配置路由规则new VueRouter({routes:[{path:'/一个命名',component:对应的组件名}]})
6. 提供组件 const   组件名={template:'  '}
7. 指定路由的出口，在页面中添加标签<router-view></router-view>,标签的位置就是将来路由中组件替换的位置

```html
<style>
    .router-link-active,.router-link-exact-active{/*router默认的两个导航高亮的类*/
        color:red;
        font-size:30px;
    }
    .now{
        color:red;
        font-size:30px;
    }
</style>
<body>
    <div id="app">
        <h1>哈哈哈</h1>
     	<ul>
          	<li><router-link to="/" exact>index</router-link></li><!--exact可以实现精准匹配-->
            <li><router-link to="/index">index</router-link></li><!--点击跳转-->
            <li><router-link to="/user">uesr</router-link></li>
        </ul>
        <router-view></router-view><!--路由中组件代替的位置-->
    </div>
    <script src="./vue.js"></script>
    <script src="./node_modules/vue-router/dist/vue-router.js"></script>
    <script>
        const Index={template:`<div>我是首页<router-link to="/index/first">first</router-link><hr/><router-view></router-view></div>`}//二级路由需要在里面再写一个路由出口，点击跳转链接要写完整
        const User={template:`<div>我是管理</div>`}
        Vue.component('index',Index)//如果只是组件中使用可以不用写这行
        const router=new VueRouter({
            routes:[
              	{path:'/',redirect: '/index'},//路由的重定向，意思是如果匹配到/则显示的是index内容
                {path:'/index',component:Index,children:[{path:'first',component:First}]},//children里面写的是二级路由，切记里面的地址前面不能加/
                {path:'/user',component:User}
              	{path:'/shop/:id'}//动态导航，根据后面的数字展示不同的内容，总的来说都是在一个页面，可以用$route.params.id拿到后面的数字。$router指的是整个项目中的路由对象，一个项目只有一个。$route指的是当前的路由规则，fullPath可以拿到#后面的东西，params可以匹配到动态路由中的数据如id，query获得的是？后面的左内容，path拿的的只是路径。里面都有一些东西，可以用{$router.参数}拿出来
            ],
         	linkActiveClass:'now',//模糊查找类，可以将默认的两个导航高亮的类重命名为别的，比如now
            linkExactActiveClass:'now'//精准查找类，可以将默认的两个导航高亮的类重命名为别的，比如now
        })
        const vm=new Vue({
            el:'#app',
          	methods:{
                fn(){
                    this.$router.push('/index')//编程式导航，可以定义点击事件，点击后如果符合条件则跳转到指定地方
                }
            },
            router:router//将路由绑定到vue实例中
        })

    </script>
</body>
```



# vue提供的十四个指令

vue指令实际上就是HTML标签特殊的属性，这些属性都是以v-开头

### v-bind：用于访问data中的数据，在标签的属性中使用

对于class和style样式很好用，简写为 :属性名。可以使用事件修饰符，时间修饰符见v-on

```vue
<div id="app" >
        <h1 v-bind:title="msg" :class="{fz:isfz}">{{msg}}</h1><!-- v-bind:title="msg"可以简写为:title="msg" -->
    </div>
    <script src="vue.js"></script>
    <script>
        const vm=new new Vue({
            el:'#app',
            data:{msg:'hello vue',isfz:true}
        })
    </script>
```



### v-model：给表单元素使用，创建双向数据绑定，当数据变了，视图也会改变，反过来同样

```vue
<div id="app" >
        <input type="text" v-model="username">     <!-- 当在文本框中输入内容时，username数据同步发生变化，使用控制台修改username值时，文本框内容同步变化-->
	<select v-model="msg"><option value="上海">上海</option><option value="北京">北京</option></select>
    </div>
    <script src="vue.js"></script>
    <script>
        const vm=new Vue({
            el:'#app',
            data:{ msg:' ',username:' '}
        })
    </script>
```



### v-on：用来给元素注册事件的，语法：v-on:事件名=“事件函数”  可以简写为@事件名

事件名：

1. click点击事件
2. dblclick双击事件

事件修饰符：@事件名.事件修饰符="事件函数"

1. .prevent阻止默认行为，比如a标签、表单的提交
2. .stop阻止冒泡
3. .capture捕获阶段执行
4. .self只有点击自己才执行，点击子元素不执行
5. .once只执行一次

注册事件经常需要阻止冒泡行为，阻止浏览器默认行为

按键修饰符：@keyup.按键修饰符="事件函数"

1. .enter
2. .esc
3. .tab
4. 如果知道某个键的ASCII可以直接写数字，如回车键就是@事件名.13

```vue
<div id="app" >
        <p>{{msg}}</p>
        <button v-on:click="clinkFn" @mouseenter="Fn">点击</button>
    </div>
    <script src="vue.js"></script>
    <script>
        const vm=new Vue({
            el:'#app',
            data:{msg:'哈哈'},
            methods: {
                clinkFn(){alert('嘻嘻')},
                Fn(){console.log('嘿嘿')}
            }
        })
    </script>
```



### v-text：更新元素的innerText属性（textContext属性）不识别标签

### v-html：更新元素的innerHTML属性，识别标签

```vue
<body>
    <div class="app">
        <h1 v-text="msg">哈哈哈</h1>
        <h1 v-html="msg">哈哈哈</h1>
    </div>
    <script src="vue.js"></script>
    <script>
        const vm=new Vue({
            el:'#app',
            data:{msg:'< a href="#"> 点我有惊喜< /a>'},
        })
    </script>
</body>
```



### v-show:用于控制某个元素的显示和隐藏

通过样式来控制显示隐藏，频繁显示隐藏用这个，有更高的初始开销

### v-if：用于控制某个元素的显示和隐藏

通过删除样式来控制显示隐藏，要不显示要不隐藏用这个，有更高的切换开销

```vue
<body>
    <div id="app">
        <h1 v-show="msg">哈哈哈</h1>
        <h1 v-if="msg">哈哈哈</h1>
    </div>
    <script src="vue.js"></script>
    <script>
        const vm=new Vue({
            el:'#app',
            data:{msg:true},
        })
    </script>
</body>
```



### v-else与v-else-if：与v-if一块使用

v-if与v-else中间不能再有别的标签内容

```vue
<body>
    <div id="app">
        <h1 v-if="msg">登录</h1>
        <h1 v-else="msg">注册</h1>
        <h2 v-if="age<=18">去网吧</h2>
        <h2 v-else-if="20>=age>=18">去酒吧</h2>
        <h2 v-else-if="age>=20">去舞吧</h2>
    </div>
    <script src="vue.js"></script>
    <script>
        const vm=new Vue({
            el:'#app',
            data:{msg:true,age:15},
        })
    </script>
</body>
```



### v-for：用于遍历一个数组或者对象

v-for是一个属性，v-for指令谁需要重复的渲染就加给谁，使用的时候一定给for后面加一个key属性且最好用id保证唯一性

1. 遍历数组：v-for="item in 数组"   item表示每次遍历出来的值，民字可以随意取
2. v-for="(item,index) in 数组"  item表示数组值，index表示下标
3. 遍历对象：v-for="item in 对象" 
4. v-for="(item,index) in 对象"

```vue
<body>
    <div id="app">
            <h1 v-for="item in msg" :key="item">{{item}}</h1>
            <h1 v-for="(item,index) in msg">{{index}}-----{{item}}</h1>
            <h2 v-for="item in sife" :key="item.id">{{item}}</h2>
            <h2 v-for="(item,index) in sife">{{index}}-----{{item}}</h2>
    </div>
    <script src="vue.js"></script>
    <script>
        const vm=new Vue({
            el:'#app',
            data:{msg:['篮球','羽毛球','乒乓球','排球'],sife:{name:'霍博涵',age:23,height:170,withe:130}},
        })
    </script>
</body>
```



### v-pre与v-once：vue碰到v-pre指令就会跳过这个标签的编译，碰到v-once会编译一次如果数据有更新视图不会改变

```vue
<h1 v-pre>hhh</h1>
<h1 v-once>xxx</h1>
```



### v-cloak：用于解决插值表达式闪烁的问题

当vue编译结束的时候，v-cloak会自己消失。真实开发中没有什么用。使用的时候需要在css中给v-cloak添加一个样式

### 自定义指令

把某个命令封装为一个自定义指令

步骤：

1. 定义一个指令（全局指令和局部指令），定义指令用directive
2. 使用这个指令 v-指令名

例如把获取焦点的操作封装为一个自定义指令

```vue
<body>
    <div id="app">
        <input type="text" v-focus><!--使用全局指令v-focus获得焦点，切记两个input框只能一个获得焦点-->
      	<input type="text" v-focus1><!--使用局部指令v-focus获得焦点-->
    </div>
    <script src="./vue.js"></script>
    <script src="./node_modules/vue-router/dist/vue-router.js"></script>
    <script>
        Vue.directive('focus',{//全局定义
            //写指令的五个钩子函数分别是：bind,inserted,update,componentUpdated,unbind
            //表示指令所在的元素插入到页面中
            //el：指的是当前元素，指令给谁加的，el就是谁
            inserted(el){
                el.focus()
            }
        })
        const vm=new Vue({
            el:'#app',
            methods:{
                fn(){
                    this.$router.push('/index')
                }
            },
          directives:{//局部指令
            focus1:{
              inserted(el){
                el.focus
              }
            }
          }
        })
    </script>
</body>
```

五个钩子函数的作用：（所有的钩子函数的参数都是一样的，具体使用看vue官网）

vue一个完整的指令是v-指令名:指令的参数.指令的修饰符.指令的修饰符="指令的值"

1. bind：只会执行一次，会在指令绑定到元素上的时候执行，此时元素不一定再页面中显示
2. inserted：所有元素插入到页面中，此时元素可以在页面中显示
3. update：当指令的值发生了改变的时候触发
4. componentUpdated：当前组所有的DOM都更新完成的时候触发
5. unbind：当指令从DOM元素上移除的时候触发

## vue中的十一个钩子函数

beforeCreate与created

beforeMount与mounted

beforeUpdata与updated

beforeDestroy与destroyed

## vue的异步DOM更新

```vue
Vue.nextTick(function(){  

console.log(document.queryselector('ul').innerHTML) 

new IScrll('.box');

 })



this.$nextTick(function(){

console.log(document.queryselector('ul').innerHTML) 

})
```



## 动态添加属性

使用$set函数

```vue
this.$set(this.car,'colir','yellow')   //第一个参数是要给那个数据属性添加属性，第二个参数是添加的属性名，第三个是添加的属性值
```

# 组件

组件是可以复用的Vue实例，所以他们与new Vue接收相同的选项，例如data,computed,watch,methods以及生命周期钩子的等。仅有的例外是像el这样根实例特有的选项。

1. 组件中不会指定el，但是会定义template。
2. 把组件当成html标签来使用
3. 定义的组件名不能是html原有的标签
4. 组件的模板中只能有一个根元素
5. Vue.component是全局组件，局部组件是写在Vue实例中的
6. 组件中的data必须是一个函数，并且函数内部要有返回值

```vue
<hello></hello>
<script>
Vue.component('hello',{//hello是第一个参数,是组件名，
	template:'<div>你好啊<button>按钮</button></div>'
  data:function(){   //数据可以修改
  	return {
  		money:100,
  		car:'hhh'
		}
	}
})
</script>
```

## 组件的另外三种定义方式

```vue
<script>
  const Index={
    template:``
  }
  Vue component('index',Index)//全局注册组件
</script>
```

```vue
<script>
  const Index={
    template:``
  }
  const vm=new Vue({
    el:'#app',
    components:{index:Index}//局部注册，Index也可以直接写入里面
  })
</script>
```

```vue
<script>
  const router=new VueRouter({
    routes:[
      {path:'/index',component:{template:``}}
    ]
  })
</script>
```



## 父传子

1. 子组件通过一个属性：props属性，可以接收到父组件传递过来的数据  props:['money','car']
2. 父组件需要给子组件传值，只需要给子组件身上增加自定义的属性<son  money="100"   :car="car"></son>

```vue
body>
    <div id="app">
        <son class="son" :car="car" :money="money"></son>
    </div>
    <script src="./vue.js"></script>
    <script>
        Vue.component('son',{
            template:`
            <div>
                <div>我是子组件</div>
                <p>{{car}}-----{{money}}</p>
            </div>`,
            props: ['money','car']  //数据不可以修改
        })
        const vm=new Vue({
            el:'#app',
            data:{
                car:'hhh',
                money:134
            }
        })
    </script>
</body>
```

## 子传父

```html
<body>
    <div id="app">
        我是父组件---{{car}}----{{money}}
        <son @sb="fn" ></son><!--需要父组件给子组件注册一个自定义事件-->
    </div>
    <script src="./vue.js"></script>
    <script>
        Vue.component('son',{
            template:`
            <div>
                <div>我是子组件</div>
                <p>{{car}}-----{{money}}</p>
                <button @click="fn">给父组件传值</button>
            </div>`,
            data:function(){
                return {money:1000,
                car:'奥迪A5'
                }
            },
            methods: {
                fn(){
                    this.$emit('sb',this.money,this.car)//子组件触发自定义事件，第一个参数：触发事件的名字。参数二：传递的参数
                }
            }
        })
        const vm=new Vue({
            el:'#app',
            data:{
                car:'',
                money:''
            },
            methods:{
                fn(money,car){//父组件需要提供一个函数
                    this.money=money
                    this.car=car
                }
            }
        })
    </script>
</body>
```

## 非父子关系（通用）

1. 创建一个bus，所有组件都能访问
2. jack组件去触发bus的一个自定义事件，传参数
3. rose给bus注册自定义事件（这个事件的时机越早越好，所以写在钩子函数中），提供一个函数，这个函数可以通过参数获取到值

```html
<body>
    <div id="app">
        <jack></jack>
        <rose></rose>
    </div>
    <script src="./vue.js"></script>
    <script>
        const bus=new Vue({})
        Vue.component('jack',{
            template:`
            <div>
                <button @click="say">jack对rose说</button>{{msg}}
                <p>rose对jack回：{{see}}</p>
            </div>
            `,
            data:function(){
                return {
                    msg:'your jump,i look',
                    see:''
                }
            },
            methods:{
                say(){
                    bus.$emit('sb',this.msg)
                }
            },
            created(){
                bus.$on('sbb',see=>{
                    this.see=see
                })
            }
        })
        Vue.component('rose',{
            template:`
            <div>
                <p>jack对rose说：{{msg}}</p>
                <button @click="fn">rose对jack回：</button>{{see}}
            </div>`,
            data:function(){
                return {
                    msg:'',
                    see:'gun'
                }
            },
            methods: {
                fn(){
                    bus.$emit('sbb',this.see)
                }
            },
            created () {
                bus.$on('sb',msg=>{
                    this.msg=msg
                })
            }
        })
        const vm=new Vue({
            el:'#app'
        })
    </script>
</body>
```

## 插槽

内容分发，会把组件中的内容分发到slot中

### 默认插槽

```html
body>
    <div id="app">
        <modal><p>确定删除</p></modal><!--modal标签中所有东西都会在slot中显示出来-->
        <modal><p>确定退出</p></modal>
        
    </div>
    <script src="./vue.js"></script>
    <script>
        Vue.component('modal',{
            template:`
            <div>
                <h1>温馨提示</h1>
                <slot></slot>
                <button>确定</button><button>取消</button>
            </div>
            `
        })
        const vm=new Vue({
            el:'#app'
        })

    </script>
</body>
```

### 具名插槽

给插槽提供一个名字<slot name="名字"></slot>

给具名插槽传内容，内容需要包括在一个template

```html
<body>
    <div id="app">
        <modal>
            <template v-slot:header>
                <h1>警告</h1>
            </template>
            <template v-slot:main>
                <p>确定删除</p>
            </template>
        </modal>
        <modal>
            <template v-slot:header>
                <h1>温馨提示</h1>
            </template>
            <template v-slot:main>
                <p>确定退出</p>
            </template>
        </modal>
        
    </div>
    <script src="./vue.js"></script>
    <script>
        Vue.component('modal',{
            template:`
            <div>
                <slot name="header"></slot>
                <slot name="main"></slot>
                <button>确定</button><button>取消</button>
            </div>
            `
        })
        const vm=new Vue({
            el:'#app'
        })

    </script>
</body>
```

### 作用域插槽

带有数据的插槽<slot name="名字" money="1000" car="玛莎拉蒂"></slot>

<template v-slot:名字="scope">

​      {{scope.money}}    显示1000

​      {{scope.car}}       显示玛莎拉蒂

</template>

```html
<body>
    <div id="app">
        <modal>
            <template v-slot:log1="a">
                <button>{{a.but}}</button>
            </template>
            <template v-slot:log2="a">
                <button>{{a.but}}</button>
            </template>
        </modal>
    </div>
    <script src="./vue.js"></script>
    <script>
        Vue.component('modal',{
            template:`
            <div>
                <h1>提示</h1>
                <p>确定退出？</p>
                <slot name="log1" :but="but1"></slot><!--:but="but1"表示传的是data中的数据，but="but1"表示传的就是but1-->
                <slot name="log2" :but="but2"></slot>
            </div>
            `,
            data:function(){
                return {
                    but1:'是',
                    but2:'否'
                }
            }
        })
        const vm=new Vue({
            el:'#app'
        })

    </script>
</body>
```

# 过渡动画

## 过渡

1. vue中提供了一个transition标签，只要将执行动画的内容包裹在这个标签里即可
   1. 配合六个类来实现效果，如果transition没有指定名字则默认六个类都是以v-开头，如果有名字则是以  名字-  开头

```html
<style>
    .v-enter,.v-leave-to{
        opacity: 0;
    }
    .v-leave,.v-enter-to{
        opacity: 1;
    }
    .v-enter-active,.v-leave-active{/*以上是默认的六个类*/
        transition: all 1s;
    }
    .fade-enter,.fade-leave-to{
        opacity: 0;
    }
    .fade-leave,.fade-enter-to{
        opacity: 1;
    }
    .fade-enter-active,.fade-leave-active{/*以上是自定义名字的六个类*/
        transition: all 1s;
    }
</style>
<body>
    <div id="app">
        <button @click="show= !show">控制显示隐藏</button>
        <transition name="fade" mode="">
            <p v-show="show">有名字的</p>
        </transition>
        <transition>
            <p v-show="show">默认的</p>
        </transition>
    </div>
    <script src="./vue.js"></script>
    <script src="./node_modules/vue-router/dist/vue-router.js"></script>
    <script>
        
        const vm=new Vue({
            el:'#app',
            data:{show:true},
            methods:{
                fn(){
                    this.$router.push('/index')
                }
            },
        })
    </script>
</body>
```

## 动画



```html
<style>
    p{
        text-align: center;
    }
    @keyframes bounce{/*bounce是自己定义的名字*/
        0%{
            transform: scale(0);
        }
        50%{
            transform: scale(2);
        }
        100%{
            transform: scale(1);
        }
    }
    .fade-enter-active{
        animation: bounce 1s ;
    }
    .fade-leave-active{
        animation: bounce 1s reverse;
    }
</style>
<body>
    <div id="app">
        <button @click="show= !show">控制显示隐藏</button>
        <transition name="fade" mode="">
            <p v-show="show">有名字的</p>
        </transition>
    </div>
    <script src="./vue.js"></script>
    <script src="./node_modules/vue-router/dist/vue-router.js"></script>
    <script>
        
        const vm=new Vue({
            el:'#app',
            data:{show:true},
            methods:{
                fn(){
                    this.$router.push('/index')
                }
            },
        })
    </script>
</body>
```

### 动画库animate css

网站(https://animate.style/)

下载安装npm install animate.css --save

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="./node_modules/animate.css/animate.css"><!--下好后引入路径-->
</head>
<style>
    h1{
        text-align: center;
    }
</style>
<body>
    <div id="app">
        <button @click="show= !show">控制显示隐藏</button>
        <transition 
        name="fade" 
        enter-active-class="animate__animated animate__bounceInLeft" 
        leave-active-class="animate__animated animate__bounceOutRight"
        ><!--enter-active-class和leave-active-class意思是自定义默认的类名，可以和动画库中的类名对应上， 不管用哪个动画都要加上animate_animated类-->
            <h1 v-show="show">有名字的</h1>
        </transition>
    </div>
    <script src="./vue.js"></script>
    <script src="./node_modules/vue-router/dist/vue-router.js"></script>
    <script>
        
        const vm=new Vue({
            el:'#app',
            data:{show:true},
            methods:{
                fn(){
                    this.$router.push('/index')
                }
            },
        })
    </script>
</body>
</html>
```

# webpack打包

1. 初始化一个项目 npm init -y

2. 安装依赖包：npm install --save-dev webpack webpack-cli

3. 在package.json文件中配置一条scripts

   "scripts":{ "build": "webpack ./src/main.js -o ./dist/bundle.js" }

   bulid是自定义的名字，webpack是使用这个依赖包，第一个地址是需要打包的是地址，第二个地址是打包后放在哪

4. 运行命令进行打包：npm run bulid

--save和--save-dev的区别：

1. --save-dev：简写-D，安装的依赖包作为开发阶段的依赖，安装的包记录到devDependencies中
2. dependencies：项目的依赖，webpack进行打包
3. devDependencies：项目开发阶段的依赖，真正上线时不需要的
4. dependencies和devDependencies都是在package中的，内容可以互换

## 使用webpack配置文件进行打包

实例：在根目录dome文件夹下创建两个文件夹，一个叫src放原始文件，一个叫dist放打包后的文件

1. 在dome下，初始化一个项目 npm init -y

2. 在dome下，安装依赖包：npm install --save-dev webpack webpack-cli

3. 在package.json文件中配置一条scripts

   "scripts":{ "build": "webpack" }

   bulid是自定义的名字，webpack是使用这个依赖包，这次不写路径

4. 在dome文件夹中创建webpack.config.js文件夹，这个文件夹是webpack默认读取的配置

5. 在src文件夹下创建main.js，app.js，index.html文件，main.js中引入app.js

   ```js
   //main.js
   require('./app')//加载app.js文件
   const $=require('jquery')//引入之前需要先下载npm add jquery
   const moment=require('moment')//npm add moment
   require('./css/index.css')//引入css文件，就不需要在html页面中引入了
   require('./less/index.less')//引入less文件，就不需要在html页面中引入了
   $(function(){
       $('li:odd').css('color','red')
       $('li:even').css('color','green')
       $('li:last').text(moment().format('YYYY-MM-DD'))
   })
   //app.js
   console.log('嘻嘻嘻')
   //index.html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <title>Document</title>
   </head>
   <body>
       <li>1我是li</li>
       <li>2我是li</li>
       <li>3我是li</li>
       <li>4我是li</li>
       <li>5我是li</li>
   </body>
   <script src="../dist/bundle.js"></script>
   </html>
   ```

   ​

6. 在webpack.config.js中写入

   ```js
   /*
       webpack.config.js文件是webpack默认会读取的配置文件，名字固定的
       webpack是运行node.js环境下的，在微博pack.config.js文件中可以使用node.js的语法
   */
   const path=require('path')//把path模块加载出来
   module.exports={
       //入口：你要对哪个文件进行打包
       entry:'./src/main.js',
       //出口：你要把文件打包到哪儿去
       output:{
           //打包的路径，一定要是绝对路径
           path:path.join(__dirname,'dist'),//node.js中的拼装路径，这句的意思是，将webpack.config.js的路径加上disk拼装起来
           filename:'bundle.js'//打包后的文件名
       },
       mode:'development'//模式：打包的模式
   }
   ```

7. 运行命令进行打包：npm run bulid

## webpack插件（官网找插件）

### html-webpack-plugin插件

```
下载安装：npm add html-webpack-plugin --save-dev
```

引入插件：const HtmlWebpackPlugin = require('html-webpack-plugin');

```js
const HtmlWebpackPlugin = require('html-webpack-plugin'); //通过 npm 安装
const webpack = require('webpack'); //访问内置的插件
const path = require('path');

const config = {
  entry: './path/to/my/entry/file.js',
  output: {
    filename: 'my-first-webpack.bundle.js',
    path: path.resolve(__dirname, 'dist')
  },
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        use: 'babel-loader'
      }
    ]
  },
  plugins: [
    new webpack.optimize.UglifyJsPlugin(),
    new HtmlWebpackPlugin({template: './src/index.html'})//html路径
  ]
};

module.exports = config;
```

## 处理css文件（直接去官网找）

style-loader

css-loader

## 处理less文件（直接去官网找）

less-loader

## 处理图片文件

file-loader或url-loade

## Babel处理浏览器js语法不兼容问题

babel-loade  （安装的时候记得看版本好，一般去原英文网站）

## 自动刷新打包

1. npm add webpack-dev-server

2. 在package.json中将自定义名字后面的webpack换成webpack-dev-server

3. npm run 自定义名字

4. 可以在webpack.config.js中配置webpack-dev-server

   ```
   devServer:{
   	open:true,
   	port:3000,
   	hot:true
   }
   ```

   ​

# ES6模块化

ES6模块化语法：

1. 导入一个模块

   import '模块名'  ，如果模块是自定义模块，需要使用相对路径

   import {导出的变量} from '模块名'，导出的变量和导入的变量一定要对应

2. 模块如何导出内容

   精准导出：export const num=10  表示导出了num变量，或者在代码的最后面统一导出export {name,num,fn}

   默认导出：

```js
//main.js
//精准导入
import vue from 'vue'
import $ from 'jquery'
import {num,name} from 'app.js'
//默认导入
import aa from 'app.js'//aa可以是任何一个名
import obj from 'app.js'//obj也可以是任何一个名
obj.num
obj.name
obj.fn()
//app.js
//精确导出
export const name=10
const num=3
function fn(){}
export {name,num,fn}
//默认导出
export default fn
export default {
  num:num,
  name,
  fn
}
```

