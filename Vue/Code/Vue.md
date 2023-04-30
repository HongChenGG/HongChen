# Vue笔记
## 1. Vue基础
### 初识Vue
 1.想让Vue工作，就必须创建一个Vue实例，且要传入一个配置对象；
 2.root容器里的代码依然符合html规范，只不过混入了一些特殊的Vue语法；
 3.root容器里的代码被称为【Vue模板】；
 4.Vue实例和容器是一一对应的；
 5.真实开发中只有一个Vue实例，并且会配合着组件一起使用；
 6.{{xxx}}中的xxx要写js表达式，且xxx可以自动读取到data中的所有属性；
 7.一旦data中的数据发生改变，那么页面中用到该数据的地方也会自动更新；
 注意区分：js表达式 和 js代码(语句)
 1.表达式：一个表达式会产生一个值，可以放在任何一个需要值的地方：

1. a
2. a+b
3. demo(1)
4. x === y ? 'a' : 'b'

2.js代码(语句)

1.  if(){}
2.  for(){}
``` Vue
   <div id="root">
        <h1>Hello,{{name}}</h1>
    </div>
    <script>
        Vue.config.silent = true;//取消 Vue 所有的日志与警告。
        //创建Vue示例
        const vm = new Vue({
            el: '#root', //El用于当前Vue示例为哪个容器服务,值通常为Css选择器字符串。
            data: {
                //data中用于存储数据,数据供El绑定的实例使用,值一般是一个对象。
                name: "尚硅谷"
            }
        })

    </script>
```
***

### Vue模板语法

Vue模板语法有2大类：

​          1.插值语法：  

​              功能：用于解析标签体内容。

​              写法：{{xxx}}，xxx是js表达式，且可以直接读取到data中的所有属性。

​          2.指令语法：

​              功能：用于解析标签（包括：标签属性、标签体内容、绑定事件.....）。

​              举例：v-bind:href="xxx" 或  简写为 :href="xxx"，xxx同样要写js表达式，

​                   且可以直接读取到data中的所有属性。

​              备注：Vue中有很多的指令，且形式都是：v-????，此处我们只是拿v-bind举个例子。

***

### 数据绑定

 Vue中有2种数据绑定的方式：

​          1.单向绑定(v-bind)：数据只能从data流向页面。

​          2.双向绑定(v-model)：数据不仅能从data流向页面，还可以从页面流向data。

​            备注：

​                1.双向绑定一般都应用在表单类元素上（如：input、select等）

​                2.v-model:value 可以简写为 v-model，因为v-model默认收集的就是value值。

***

### El与data的两种写法

 data与el的2种写法

​          1.el有2种写法

​                  (1).new Vue时候配置el属性。

​                  (2).先创建Vue实例，随后再通过vm.$mount('#root')指定el的值。

​          2.data有2种写法

​                  (1).对象式

​                  (2).函数式

​                  如何选择：目前哪种写法都可以，以后学习到组件时，data必须使用函数式，否则会报错。

​          3.一个重要的原则：

​                  由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this就不再是Vue实例了。

```vue
<script type="text/javascript">
		Vue.config.productionTip = false //阻止 vue 在启动时生成生产提示。

		//el的两种写法
		/* const v = new Vue({
			//el:'#root', //第一种写法
			data:{
				name:'尚硅谷'
			}
		})
		console.log(v)
		v.$mount('#root') //第二种写法 */

		//data的两种写法
		new Vue({
			el:'#root',
			//data的第一种写法：对象式
			/* data:{
				name:'尚硅谷'
			} */

			//data的第二种写法：函数式
			data(){
				console.log('@@@',this) //此处的this是Vue实例对象
				return{
					name:'尚硅谷'
				}
			}
		})
	</script>
```

***

### MVVM模型

​    MVVM模型

​            1. M：模型(Model) ：data中的数据

​            2. V：视图(View) ：模板代码

​            3. VM：视图模型(ViewModel)：Vue实例

​      观察发现：

​            1.data中所有的属性，最后都出现在了vm身上。

​            2.vm身上所有的属性 及 Vue原型上所有属性，在Vue模板中都可以直接使用。



