1. 在浏览器中储存数据：

   （1）永久性普通储存：localStorage.setItem('key', "value");key是保存的名字，value是需要保存的数据

   （2）永久性数组储存：localStorage.setItem('key', JSON.stringify(data));data就是需要储存的数组

   （3）临时性普通存储：sessionStorage.setItem('key', "value");窗口关闭则数据清空

   （4）临时性数组储存：localStorage.setItem('key', JSON.stringify(data));data就是需要储存的数组

2. 在浏览器中取出数据：

   （1）永久性普通取出：localStorage.getItem('key');key是保存的名字

   （2）永久性数组取出：数组名=JSON.parse(localStorage.getItem('data'));



# 事件

1. but.removeAttribute('disabled');创建一个事件删除某个元素的指定属性


# 对于字符串的操作

1. substr('起始的位置',截取几个字符)
2. split('=')    可以利用自己指定的字符分割字符串，返回的是一个数组
3. 字符串名.slice(0,1)意思是去字符串的第一个字符，如果只写一个参数意思是从第几个一直取到最后一个

# 对于数组和对象的操作

1. 数组名.reverse()方法可以翻转数组

2. 数组名.join(' ')可以拼接数组为字符串

3. 数组名.slice(0,1)意思是取数组的第一个，如果只写一个参数意思是从第几个一直取到最后一个

4. 数组名.splice(数组下标,删除几个)意思是从第几个下标开始删除，一共删除几个元素

5. findIndex()：返回第一个满足条件的下标

6. find()：返回第一满足条件的元素

7. unshift()：方法将新项添加到数组的开头，并返回新的长度。比如：list.unshift({id:+new Date(),name:this.todoName,flag:false})

8. push()：方法将新项添加到数组的结尾，并返回新的长度。

9. 过滤数组this.list=this.list.filter(item => item.id !== id)只把id不同的留下

   数组名.some(item=>item.布尔值)只要有一个布尔值是true就返回true

   数组名.every(item=>item.布尔值)全部的布尔值是true就返回true

   数组名.forEach() 方法对数组的每个元素执行一次提供的函数。