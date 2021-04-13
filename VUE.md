<!-- 个人看法:方法与计算属性不同 -->
<!-- 方法:主要用书写一些逻辑代码 -->
<!-- 计算属性:通过return 返回一些数据，也相对于是一个变量，只不过进行一些处理 -->

<!-- 响应式 -->
<!-- vue CLI2 使用的为Object.defineProperty:数据劫持，要对每个对象的值进行一一绑定 -->
<!-- vue Cli3 使用的为const pro = new Proxy(对象,{set(obj,key,value),get(obj,key)})数据代理，该proxy的实例化对象进行该对象的代理对象，要想对该对象进行监视，就必须调用代理来修改，添加值，只用对对象进行绑定，不用对对象中的每一个值进行绑定 -->

通过vue的实例化对象进行声明式编程:new Vue({})
<!-- 在标签中使用全局变量时要使用$进行修饰，否则就会该参数当做模板内的变量使用 -->
<!-- 实例化对象中要调用变量通过this点进行调用 -->
el:获取到要进行管理的标签,一个字符串
data:用来定义和声明变量,一个对象//采用了
computed:计算属性,对数据进行二次封装或者改变,或者对多个变量进行计算，存在缓冲，相对于methods，computed的性能要好一些，不存在参数
motheds:用来定义书写函数
watch:用来监听变量，只要有变量的值发生改变后就会触发，一般跟v-model连用
props:用来接收父代向子代传递的变量，如果在props中没有接收到父传递的参数，此参数就会出现到该实例的$attrs中

<!-- 在标签中可以使用对象或者数组表示一个属性有多个的值，一般使用在class中 -->
<!-- style:动态赋值里面的样式通过对象的形式进行赋值 如{color:'pink'} -->

标签中的语法:{
    <!-- 在标签中使用vue中的变量直接写变量名 -->
    表达式:{
        v-for=(item:可迭代对象中的值,index:索引值) in array<=>将可迭代对象进行循环显示，当遍历的为对象时(value:对象的value,key:对象的key,index) in obj:{
            遍历数组时，通过array[0] = 1;来修改数组的值没有效果，可以通过splice来进行修改值
        }
        v-on:事件类型=事件函数|执行代码如v-on:click，**语法糖**@事件名，如@click<=>为标签绑定事件,参数传递:{
            当没有参数时在标签中可以省略括号
            当函数中需要参数但是在调用时没有传递参数，该参数为event
            当在调用时有参数传入时，event参数必须在调用使用$event代替
        },修饰符:{
            .stop:阻止事件冒泡
            .prevent:阻止默认事件
            .{keyCode:键的ASCII码|keyAlias:键的别名，就是a~w}
            .native:让组件可以绑定事件
            .once:该事件只会触发一次
        }
        v-html="变量"<=>会自动将字符串进行解析如果为HTML文档格式会解析后显示
        v-text="变量名"<=>跟mustache语法一样，只是v-text写在标签内部
        v-bind:src="www.baidu.com"<=>为标签中的属性进行动态赋值，**语法糖**:属性，如:src
        v-if=Boolean<=>使用在同级标签中，只能显示一个，并且该在DOM树中只会渲染显示的标签，没有显示的标签不会进行渲染也就是直接删除不显示的标签
        v-else-if=Boolean<=>使用在同级标签中，只能显示一个，并且该在DOM树中只会渲染显示的标签，没有显示的标签不会进行渲染也就是直接删除不显示的标签
        v-else<=>没有Boolean该标签的显示取决于v-if和v-else-if是否显示，使用在同级标签中，只能显示一个，并且该在DOM树中只会渲染显示的标签，没有显示的标签不会进行渲染也就是直接删除不显示的标签
        在v-if中的标签使用可以来表示是否将该标签重新渲染，而不是像之前的替换
        v-show=Boolean<=>跟v-if差不多，只是当为false时，该标签只是将css中display设置为了none
        v-model="变量"<=>使用在input标签中实现双向绑定，在type为radio或者CheckBox中使用了v-model就可以不用使用name属性，当type为CheckBox要使用一个数组类型的变量,修饰符:{
            .lazy:懒加载，在使用v-model后在input标签中有按下回车或者失焦才会进行数据绑定
        }
    }
    指令:{
        <!--直接使用 <a v-once></a> -->
        v-once:表示当第一次赋值后就不会对该标签中的变量进行监听 
        v-pre:表示为vue在该标签中的插值语法失效,包括其后代标签
    }
}

VUE的生命周期{
    create 创建 -------- 创建vue实例并初始化,用来进行网络数据请求,但是不能获取到标签
    mount 挂载 -------- 把vue实例和视图进行关联
    update 更新 ------- 监听数据与视图的变化
    destroy销毁 ------- 销毁实例
    beforeCreate:在实例初始化之后，数据观测（data observer）和event/watcher事件配置之前调用，里面的this指向实例
    created:实例已经创建完成之后被调用。在这一步，实例已完成以下的配置；数据观测（data observer),属性和方法的运算，watch/event事件回调。然而，挂载阶段还没开始，还未与页面关联起来，$el属性目前不可见。可在这阶段进行一些初始化的操作（如ajax获取数据之类的），，此时vue的对象已经创建成功，可以访问vue中的数据和方法，但是还没有创建好虚拟DOM
    beforeMount:在挂载之前没调用，解析模板，把实例对象下的$el属性指向设置中的el参数指定的元素，这个解析后的模板还没有和$el进行绑定，此时的虚拟DOM已经创建完毕，还没创建好真实DOM
    mounted:挂载之后调用，把解析后的模板与页面元素进行绑定，用解析后的模板内容替换页面，真实DOM创建完成
    beforeUpdate:在数据绑定之前被调用
    updated:在数据改变之后被调用，可以进行依赖于dom的操作（可以在这个阶段进行dom操作）

    activated:处于活跃状态
    deactiveated():即将不活跃
}

插值操作:{
    <!-- 将vue中data中的变量在HTML标签中显示 -->
    mustache:胡须语法,也是双大括号语法{{message}}，在mustache中还可以进行变量的拼接，就像字符串一样使用{{ message + " " + age}}
    v-html="变量名":会自动将字符串进行解析如果为HTML文档格式会解析后显示
    v-text="变量名":跟mustache语法一样，只是v-text写在标签内部
}

父子组件通信:{
    props:父向子传，在自定义标签中写<tem :name="name">props:{
        每个变量都可以定义三个属性:{
            type:类型[string|number|object],当定义的类型为复杂数据类型时，赋默认值必须通过工厂函数来获取，及一个函数返回值，形成闭包保护数据
            default:"djfsdk",默认值
            required:boolean=>是否该值必须传递
        }
    }
    emit:子向父传:{
        在子组件中发射一个事件，通过this.$emit("自定义事件名",参数)，然后在使用子组件中去监听该自定义的事件
    }
}

$children:用来显示所有的子组件，在实例化中通过this.$children一个数组包括该组件中的所有的子组件
$parent:来访问组件的父组件
$root:用来访问根组件
$el:得到该组件标签
$ref="name":表示为来获取到组件或者标签，通过this.$refs.name来进行调用

$nextTick(function):运用在生命周期函数中，表示为在该生命周期的下一个生命周期实现，其实就相当于一个定时器setTimeout(()=>{},17)
$data:可以获取到data中的值,data中绑定的属于数据在vue实例中也都包含
$options:可以获取到vue中所有的信息
$set(this.obj,"age",100):为data中的obj对象添加一个值，并为该值赋值，才会实现响应式
$attrs:一个对象，对象中的值为从父组件中传递到子组件中的值，当在props中没有接收该值时，该值会被添加到$attrs对象中

还有定义在vue中的所有的数据
__proto__

自定义vue全局函数:{
    1.在main.js中创建:Vue.prototype.$名字 = funtion(){}，不要使用箭头函数，不然该this指向不对，使用prototype是将函数挂载到全局
    2.可以在每个组件通过this来进行调用，因为没有this都是一个vue实例化对象，并且在该函数中的this就是每个实例化对象中的this
    3.this:{
        data:中每个值都一一列出
        methods:中每个方法都一一列出
        computed:中每一个计算属性都一一列出
        
    }
}

slot:插槽{
    使用在组件中，当成一个slot标签使用
    默认插槽，当在组件中没有添加标签就使用默认的标签
        <div>
            <p>Lorem ipsum dolor sit amet.</p>
            <p>Lorem ipsum dolor sit amet.</p>
            <slot><div>dsklfjsdklj</div></slot>
        </div>
    具名插槽:在组件中要使用标签替换插槽必须在标签中添加slot属性，并且属性值要和替换的插槽中的name属性值一样
        <div>
            <p>Lorem ipsum dolor sit amet.</p>
            <p>Lorem ipsum dolor sit amet.</p>
            <slot name="hou"></slot>
        </div>
    具名默认插槽
        <div>
            <p>Lorem ipsum dolor sit amet.</p>
            <p>Lorem ipsum dolor sit amet.</p>
            <slot name="hou"><div>dsklfjsdklj</div></slot>
        </div>
    具名插槽:在slot标签中添加name属性和属性值:{
        在要替换的标签中添加slot属性和slot标签中对应的属性值
    }
}

vue 脚手架2:创建项目:vue init webpack 项目名称
vue 脚手架3:创建项目:vue create 项目名称
vue 脚手架4:创建项目:npm init vite-app 项目名称

下载插件:1.npm install 插件名称 --save:运行时依赖
         2.npm install 插件名称  --save-dev:开发时依赖

vue router:{
    插件名称:vue-router,运行时依赖
    使用:{
        1.先要导入该插件:import vueRouter from "vue-router"
        2.导入Vue的实例化对象:import Vue form "vue"
        3.安装挂载插件:Vue.use(插件)
        4.创建VueRouter实例化对象:{
            在实例化对象中的参数:{
                1.routes:[]=>{
                    <!-- 定义多个路由对象---route -->
                    path:显示的路径
                    component:显示组件
                    <!-- 以上必写 -->
                    meta:一个对象可以自定义一些变量进行存放，调用
                    name:定义组件的名字，没有强制要求
                    fullPath:路径名，route对象自动赋值
                    matched:[]一个数组
                    params:{}携带路由跳转时的参数,该参数为url后面的动态路由
                    query:{}携带路由跳转时的参数,该参数为url后面&后面的数据
                }
                2.history:hash|history:设置url路径的显示，设置为hash时有url中包含#,history中为h5的新特效
                3.linkActiveClass:"类名"，给正在显示的路由添加一个类名
            }
        }
        5.在app.vue中配置:{
            router-link:用于跳转路由:{
                1.tag:默认将router-link转化为a标签，使用该属性后将该组件改变为自己定义的标签
                2.replace:跳转后不会进入history的栈内存中，一个Boolean属性
                3.active-class:当正在使用该组件时会自动给组件增加一个类名，可以自己设定，默认为router-link-active类名
                4.to:指定跳转的路径，必写
            }
            router-view:用于路由的显示页面
        }
        6.在路由中设置默认路径:{
            在vue-router实例化中的routes数组中添加一个:{
                path:"/",redirect:要显示组件的路径
            }
        }
    }
    动态路由:{
        只用在path中{path:"/user/:id"}后面的id就动态进行赋值的
        获取动态的信息:通vue实例化中的route
    }
    <!-- 导航守卫还可以定义在route对象中成为路由独享守卫=>前置钩子:beforeEnter-->
    导航守卫前置钩子:{
        定义在router实例化对象中的:{
            beforeEach((to:到什么路由地址,from:从什么路由地址来,next({path:"":表示跳转到指定的路由}:该参数默认不写):一个函数必须调用)=>{
                <!-- 设置title:document.title = to.meta.title -->
                to:将要到路由的route对象
                from:现在的路由route对象
                next();
            })
        }
    }
    导航守卫后置钩子:{
        定义在router实例化对象中的:{
            afterEach((to:route,from:route)=>{
                <!-- 设置title:document.title = to.meta.title -->
                to:将要到路由的route对象
                from:现在的路由route对象
            })
        }
    }
}

二级路由:{
    1.在父代路由对象添加一个children属性，该属性就相当于routes来进行配置同样也是path(路径不能加/)，component，设置默认路径还是用redirect
    2.在父组件中还是要包含router-view等标签
}

vue实例化中的属性:{
    <!-- router是自己在vue中定义的 -->
    1.$router:实现路径的跳转{
        1.push('路径'):跳转到指定路径
        2.replace('路径'):跳转到指定路径,但是不会进入history中的栈内存
        还可以将路径改为对象方便传递参数:{
            1.path:跳转的路径
            2.query:{}=>url地址中?后面带的参数
        }
    }
    <!-- route是在router实例化中的routes中单个实例化对象，此处为处于活跃状态下的route -->
    2.$route:处于活跃状态下的route{
        获取动态路由:params.设置的变量名
        获取url中的参数:query.设置的变量名
    }
}

路由懒加载:const a = ()=>import(组件路径)

keep-alive:保持活性=>将router-view标签写在keep-alive:标签中{
    <!-- include和exclude中存放的为在组件中定义的name属性的值，多个使用逗号进行分割 -->
    include:参数为字符串或者正则表达式，只有满足include中的才会进行缓存
    exclude:参数为字符串或者正则表达式，只有不满足exclude中的才会进行缓存
}

在组件中使用路由守卫:beforeRouteLeave(to,from,next){}=>在该守卫中可以使用this表示为该组件

<!-- 下载:npm i vuex --save -->
vuex:{
    1.先要导入该插件:import vueRouter from "vue-router"
    2.导入Vue的实例化对象:import Vue form "vue"
    3.安装挂载插件:Vue.use(插件)
    4.实例化对象:new vuex.Store({
        <!-- state:用来存放变量 -->
        <!-- 调用:this.$store.state.变量，不能对变量进行修改 -->
        state:{a:"dsfks"},
        <!-- mutations用来中定义函数，参数=>第一个参数state:就是state变量，可以调用其中的变量，第二个参数:调用时传递的参数，可以多个 -->
        <!-- 调用:this.$store.commit(函数名,参数名) -->
        <!-- 进行异步操作 -->
        mutations:{},
        <!-- getters=>用来定义计算属性，第一个参数state:就是state变量，可以调用其中的变量，第二个参数为getters，可以调用其中的计算属性 -->
        <!-- 调用:this.$store.getters.函数名():有参数时可以写括号，没有参数括号可以省略 -->
        <!-- 要想获取组件调用时传递的参数必须=>return function(参数){书写代码} -->
        getters:{},
        <!-- actions进行异步操作，参数=>第一个参数content:就是store实例化对象，可以调用其中的变量，第二个参数:调用时传递的参数，可以多个  -->
        <!-- 调用this.$store.dispatch(函数名,参数) -->
        <!-- 要修改state中变量的值，还是要通过mutations来进行修改 -->
        actions:{},
        <!-- modules:定义模块，可以在modules中在定义state，mutations，getters... -->
        <!-- moulde中state:调用this.$store.state.模块名.变量名 -->
        <!-- moulde中mutations:调用this.$store.commit(函数名,变量名)模块中的函数名不要跟其他mutations中的函数名重复 -->
        <!-- moulde中getters:调用this.$store.getters.计算属性(),模块中的计算属性名不要跟其他getters中的计算属性名重复 -->
        modules:{}
    })
    5.导出
    6.在vue中进行定义:将vuex定义为store
    <!-- 辅助函数 -->
    mapState:state的映射函数,mapMutations:mutations的映射函数,mapGetters:getters的映射函数,mapActions:actions的映射函数
    导入:vuex导入import { mapState, mapMutations, mapGetters, mapActions } from "vuex"
    激活:...mapState(["变量名"])=>在computer中激活，
         ...mapGetters(["变量名"])=>在computer中激活，
         ...mapMutations(["变量名"])=>在methods中激活，
         ...mapActions(["变量名"])=>在methods中激活
    使用:通过this.变量名调到
}

<!-- 下载npm i axios --save -->
axios:{
    <!-- 自己理解:因为不需要在vue中使用axios实例化对象，所有不要将axios挂载到vue实例化对象中 -->
    1.先要导入该插件:import axios from "axios"
    2.axios:{
        1.axios()=>原始请求
        2.axios.get|post...()=>指定请求方法
        3.axios.all([]).then(reslut=>{})=>可以在数组中存放多个axios对象一次进行多个数据请求，result为一个数组请求后得到的资源
        <!-- 拦截器 -->
        1.interceptors.response.use(res=>{}:成功的回调函数,err=>{}:失败的回调函数):数据返回的拦截器
        2.interceptors.request.use(res=>{}:成功的回调函数,err=>{}:失败的回调函数):请求发送的拦截器
        <!-- 使用拦截器后，必须还要将参赛return出去，让请求继续进行 -->
        在axios中的请求设置的参数:{
            1.url:"",必写
            2.method:"get|post|...",默认get
            3.params:{key:value}:GET方式请求?后面参数进行拼接
            4.data:{}:POST方法请求
        }
    axios请求设置的其他属性:{
        baseUrl:设置基本路径，设置基本属性后url就只用写后面部分
        timeout:设置超时时间
    }
    axios.defaults.属性:设置axios全局属性，设置好后相当于在每个axios对象中都配置了该属性
    axios.create():在创建一个跟axios一样的实例化对象，通过这个create创建的对象也可以使用all(),get|post();等axios对象的方法

    axios对象无论调用那个用来请求数据的函数都可以在通过.then.catch来设置成功和失败的回调函数
    }
}

vue.config.js文件配置:{
    module.export = {
        publicPath:{type:String,defalut:"/"},//设置公共路径，由于打包后路径和在线运行路径不一样，使用要使用三目运算
        <!-- publicPath: process.env.DEMO_ENV == "production" ? "./" : "/", -->process.env.DEMO_ENV使用这个参数要创建.env.development和.env.production连个文件具体区别看该两个文件
        outputDir:{type:String,default:"dist"},配置打包后的文件名
        assetsDir:{type:String,default:""},打包后静态文件的位置
        filenameHashing:boolean,打包后文件名后面是否要上哈希值
        indexPath:"index.html",打包后的进入文件的名字
    }
}

bus{
    挂载:vue.prototype.$bus = new vue();
    传值:{
        this.$bus.$emit("函数名","参数")
        this.$bus.$on("函数名",function(value){
        　　console.log(value)
        })
    }
}

.env 全局默认配置文件，不论什么环境都会加载合并

.env.development 开发环境下的配置文件,npm run serve调用

.env.production 生产环境下的配置文件,npm run build

2，关于内容

　　注意：属性名必须以VUE_APP_开头，比如VUE_APP_XXX

3，关于文件的加载：

　　根据启动命令vue会自动加载对应的环境，vue是根据文件名进行加载的，所以上面说“不要乱起名，也无需专门控制加载哪个文件”

　　比如执行npm run serve命令，会自动加载.env.development文件


<!-- vue动画 -->
运用场景:v-if,v-show,路由
使用:{
    将要进行vue动画的标签使用transition标签包裹
    在transition中添加一个name属性
    在css中通过进入:.name中的值-enter{要进入时的样式},-enter-active{在进入时到进入后之间的过渡},-enter-to{进入后的样式}
               离开:.name中的值-leave{要离开时的样式},-leave-active{在离开时到离开后之间的过渡},-leave-to{离开后的样式}
}

第三方插件:[
    1.fastclick:作用取消手机端300ms延迟，在css中可以通过touch-action:manipulation,在HTML页面中通过meta设置name为viewport，content为width=device-width,initial-scale=1
    2.hammerJs:手机端的手势插件
]