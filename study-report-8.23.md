># Vue.js目录结构

目录         |说明
------------ |--------------
build        | 项目构建(webpack)相关代码
config       |配置目录，包括端口号等。我们初学可以使用默认的。
node_modules |npm 加载的项目依赖模块
src          |这里是我们要开发的目录，基本上要做的事情都在这个目录里。  里面包含了几个目录及文件：- assets:放置一些图片，如logo等。- components: 目录里面放了一个组件文件，可以不用。- App.vue: 项目入口文件，我们也可以直接将组件写这里，而不使用 components 目录。- main.js: 项目的核心文件。  
static        |静态资源目录，如图片、字体等。
test          |初始测试目录，可删除
.xxxx文件     |这些是一些配置文件，包括语法配置，git配置等。
index.html    |首页入口文件，你可以添加一些 meta 信息或统计代码啥的。
package.json  |项目配置文件。
README.md     |项目的说明文档，markdown 格式  
<br>
<br>

>## Vue.js条件语句 

v-if 指令用于条件性地渲染一块内容。这块内容只会在指令的表达式返回 truthy 值的时候被渲染。也可以用 v-else 添加一个“else 块”。也可以使用v-else-if，充当 v-if 的“else-if 块”，可以连续使用：  
```html
    <div v-if="type === 'A'">
    A
    </div>
    <div v-else-if="type === 'B'">
    B
    </div>
    <div v-else-if="type === 'C'">
    C
    </div>
    <div v-else>
    Not A/B/C
    </div>
```
<br>
<br>

>## Vue.js循环语句  

我们可以用 v-for 指令基于一个数组来渲染一个列表。v-for 指令需要使用 item in items 形式的特殊语法，其中 items 是源数据数组，而 item 则是被迭代的数组元素的别名。  v-for 还支持一个可选的第二个参数，即当前项的索引。  
```html
<ul id="example">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>  
```
```javascript
var example = new Vue({
  el: '#example',
  data: {
    parentMessage: 'Parent',
    items: [
      { message: 'Foo' },
      { message: 'Bar' }
    ]
  }
})
```
<br>
<br>

>## v-bind 

动态地绑定一个或多个 attribute，或一个组件 prop 到表达式。  
```html
<!-- 绑定一个 attribute -->
<img v-bind:src="imageSrc">

<!-- 缩写 -->
<img :src="imageSrc">
```
<br>
<br>

>## Vue.js组件  

组件是可复用的 Vue 实例。  
```html
    <div id="app">
        <ul>
            <school v-for="item,index in schoolList" :action='changeEvent' :key="index" :index="index" :school-name="item"></school>
        </ul>
        <h2>选中的学校是：{{chooseSchool}}</h2>
    </div>
```
```javascript
<script type="text/javascript">
    Vue.component("school",{
        props:['schoolName','index','action'],
        template:`<li>
                        <h3>{{index}}-学校名称：{{schoolName}}</h3>
                        <button @click="$parent.chooseSchool = schooleName">选择学校</button>
                    </li>`,
        methods:{
            chooseEvent:function(schoolName){
            }
        }
    })
    //根组件
    let app = new Vue({
        el:"#app",
        data:{
            schoolList:['清华','北大','浙大','中大'],
            chooseSchool:""
        },
        methods:{
            changeEvent:function(data){
                this.chooseSchool = data
            }
        }
    })
```
<br>
<br>

>## v-model  

可以用 v-model 指令在表单 input、textarea 及 select 元素上创建双向数据绑定。  
```html
    <div id="app">
        <input-com v-model="username"></input-com>
        <h3>{{username}}</h3>
    </div>
```
```javascript
    <script type="text/javascript">
        Vue.component('input-com',{
            props:['username'],
            template:`<input type="text" @input = "$emit('child-input',$event.target.value)" :value="username" />`,
        })
        
        let app = new Vue({
            el:'#app',
            data:{
                username:""
            },
            methods:{
                changeEvent:function(data){
                    this.username = data
                }
            }
        })
```
<br>
<br>

>## Vue.js路由  

Vue.js 路由允许我们通过不同的 URL 访问不同的内容。
通过 Vue.js 可以实现多视图的单页Web应用.
```javascript
const NotFound = { template: '<p>Page not found</p>' }
const Home = { template: '<p>home page</p>' }
const About = { template: '<p>about page</p>' }

const routes = {
  '/': Home,
  '/about': About
}

new Vue({
  el: '#app',
  data: {
    currentRoute: window.location.pathname
  },
  computed: {
    ViewComponent () {
      return routes[this.currentRoute] || NotFound
    }
  },
  render (h) { return h(this.ViewComponent) }
})
```  

以上只是随便罗列了几个感觉常用到的，最近才终于把Vue框架给看完，但是感觉也只是看过而已，没实战也不怎么会用，然后现在才开始准备暑假考核QAQ，希望能按时完成暑假考核叭。