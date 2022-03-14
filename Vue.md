# Vue开发（2.0）

## 一、Vue对象基础

### 1.Vue对象实例属性

 	1.el属性：

```javascript
//指定Vue对象的挂载DOM
let vue = new Vue({
    el:'#app'
})
```

 	2.data属性：

```javascript
//页面中所用到的数据,该属性下的数据都是响应式的，可用于页面数据绑定
let vue = new Vue({
    el: '#app',
    data(){
        return {
        	a:'123'
    	}
    }
})
```

 	3.methods属性：

```javascript
//methods属性用于定于所需要调用的方法、及回调函数
let vue = new Vue({
    el: '#app',
    data(){
        return {
        	a:'123'
    	}
    },
    methods:{
        login () {
            console.log('123')
        }
    }
})
```

 	4.computed属性：

```javascript
//computed是一个计算属性、与data中的数据一样，以变量的形式调用
let vue = new Vue({
    el: '#app',
    data(){
        return {
        	a:'123'
    	}
    },
    methods:{
        login () {
            console.log('123')
        }
    },
    computed:{
        conls(){		//当依赖的数据变化时自动调用
            console.log(this.a)
        }
    }
})
```

 	

```javascript
//computed的get和set方法
let vue = new Vue({
    el: '#app',
    data(){
        return {
        	a:'123'
    	}
    },
    methods:{
        login () {
            console.log('123')
        }
    },
    computed:{
        conls:{
            get(){
                return this.a
            }
            set(newVal){
        		this.a = '456'
    		}
        }
    }
})
```

 	5.watch属性：

```javascript
//watch可以监听data属性中数据的变化
//computed的get和set方法
let vue = new Vue({
    el: '#app',
    data(){
        return {
        	a:'123'
    	}
    },
    methods:{
        login () {
            console.log('123')
        }
    },
    computed:{
        conls:{
            get(){
                return this.a
            }
            set(newVal){
        		this.a = '456'
    		}
        }
    },
    watch:{
    	a(oldVal,newVal){		//watch中的方法名与data中的变量名一致，表示要监听的数据
    		console.log(this.a)
		}
    }
})
```

 	

```javascript
//watch属性深度监听
//watch可以监听data属性中数据的变化
//computed的get和set方法
let vue = new Vue({
    el: '#app',
    data(){
        return {
        	a:'123',
            b:{
                a:'123',
                b:'456'
            }
    	}
    },
    methods:{
        login () {
            console.log('123')
        }
    },
    computed:{
        conls:{
            get(){
                return this.a
            }
            set(newVal){
        		this.a = '456'
    		}
        }
    },
    watch:{
    	a(oldVal,newVal){		//watch中的方法名与data中的变量名一致，表示要监听的数据
    		console.log(this.a)
		},
        b:{
            handler(newVal,oldVal){
                console.log(newVal)
            },
            immediate: true,
            deep:true		//开启深度监听
        }
    }
})
```

 	6.filters属性：

```javascript
//filters用于对数据进行过滤
let vue = new Vue({
    el: '#app',
    data(){
        return {
        	a:'123',
            b:{
                a:'123',
                b:'456'
            }
    	}
    },
    methods:{
        login () {
            console.log('123')
        }
    },
    computed:{
        conls:{
            get(){
                return this.a
            }
            set(newVal){
        		this.a = '456'
    		}
        }
    },
    watch:{
    	a(oldVal,newVal){		//watch中的方法名与data中的变量名一致，表示要监听的数据
    		console.log(this.a)
		},
        b:{
            handler(newVal,oldVal){
                console.log(newVal)
            },
            immediate: true,
            deep:true		//开启深度监听
        }
    }，
    filters:{
        toUpper(letter){
            return letter.toLocaleUpperCase()
        }
    }
})
```

 	7.components属性：

```javascript
//components属性对定义的组件进行注册，以供使用
import children from "./children.vue"
let vue = new Vue({
    el: '#app',
    data(){
        return {
        	a:'123',
            b:{
                a:'123',
                b:'456'
            }
    	}
    },
    methods:{
        login () {
            console.log('123')
        }
    },
    computed:{
        conls:{
            get(){
                return this.a
            }
            set(newVal){
        		this.a = '456'
    		}
        }
    },
    watch:{
    	a(oldVal,newVal){		//watch中的方法名与data中的变量名一致，表示要监听的数据
    		console.log(this.a)
		},
        b:{
            handler(newVal,oldVal){
                console.log(newVal)
            },
            immediate: true,
            deep:true		//开启深度监听
        }
    }，
    filters:{
        toUpper(letter){
            return letter.toLocaleUpperCase()
        }
    },
    components:{
        children
    }
})
```



### 2.Vue生命周期

beforeCreate

created

beforeMount

mounted

beforeUpdate

updated

beforeDestroy

destroyed

### 3.Vue组件

### 4.VueAPI

## 二、Vue指令

## 三、Vue-Router

## 四、vuex

## 五、代理解决跨域

```js
module.exports = {  
    /* 部署生产环境和开发环境下的URL：可对当前环境进行区分，baseUrl 从 Vue CLI 3.3 起已弃用，要使用publicPath */  
    publicPath: "",  
    assetsDir: "static/lipin",  
    outputDir: "dist",  
    runtimeCompiler: true,  
    productionSourceMap: false,  
    /* webpack-dev-server 相关配置 */  
    devServer: {  
        /* 自动打开浏览器 */  
        open: true,  
        /* 设置为0.0.0.0则所有的地址均能访问 */  
        host: "127.0.0.1",  
        port: 8080,  
        https: false,  
        hotOnly: false,  
        /* 使用代理 */  
        proxy: {  
            '/': {  
                /* 目标代理服务器地址 */  
                target: "http://localhost:8081",  
                /* 允许跨域 */  
                changeOrigin: true,  
            },  
        },  
    },  
} 
```

