<!-- render:就是将通过js编译成虚拟DOM，然后在通过mount挂载到真实DOM中 -->
<!-- ref:使用在标签中的，不是VUE3中的ref模块，ref写的标签中是给标签一个标识，然后在虚拟DOM中进行特殊化处理，在vue通过ref标识的名字方便操作虚拟DOM，然后和真实DOM进行对比，将不同的地方在真实DOM中进行修改 -->
<!-- vue2.0中操作虚拟DOM:this.$refs.标识的名字 -->
<!-- vue3.0中操作虚拟先在setup中定义一个变量初始值可以有也可以没有，然后在ref的标识的名字跟setup中的名字一样，就可以直接将该虚拟DOM对象的标签赋值给该变量，原来该变量的值就直接被覆盖，在js中直接使用该变量.value就可以直接修改和查看该虚拟DOM=>这个就是ref函数的属性 -->

<!-- 当在父代中要查看子类中的数据，如果没有发现数据没有改变，但在子类中查看时发生改变了，此时要通过异步函数进行访问，settimeout来进行调用 -->
<!-- 在setup中定义的变量或者进行监听的变量并不会挂载到该vue实例中只要return出来的数据才会进行挂载到vue实例中 -->
<!-- 在vue3或者vite中数组的是可以监听的，当直接改变数组的值时也是响应式 -->
<!-- 父子中生命周期的执行顺序:F:beforeCreate->F:created->F:beforeMounte->S:beforeCreate->S:created->S:beforeMounte->S:mounted->F:mounted -->
<!-- vue在mounted生命周期中父组件中调用子组件中的变量时如果该变量是通过其他插件进行实例化的有可能该组件还没有实例化成功，所有要通过setTimeout异步调用 -->

<!-- vue2.X中为options api就是将各个接口定义在组件中 -->
<!-- vue3.0中为composition api:就是将各个接口定义在vue中需要什么就从vue中导出 -->

<!-- setup中return的原因:1.将return的变量或者函数挂载到实例中在其他组件中只能访问我return出去的变量或者方法，包含数据。2.告诉render在绘制虚拟DOM时要注意我return出去的变量方便挂载到真实DOM中 -->

vite实例化对象中可以定义的属性:{
    name:"",
    setup:函数,定义变量和函数
    emit:数组,对自定义事件进行注册
    props:对象|数组,对父组件传递的参数做接收
    components:对象,对子组件进行注册
}


个人认为 vue3.0 更加趋向于模块化开发，按需引入
vue3.0 在数据响应式上使用了 js 中代理模式=>new Proxy(对象,{get,set}):可以对整个对象进行监听
vue2.0 中的数据劫持 Object.defineProperty():只能对基本数据内心进行监听，如果是对象，要通过 foreach 进行逐个监听

1、virtual DOM 完全重写，mounting & patching 提速 100%；
虚拟dom是
2、更多编译时 （compile-time）提醒以减少 runtime 开销；
3、基于 Proxy 观察者机制以满足全语言覆盖以及更好的性能；
4、放弃 Object.defineProperty ，使用更快的原生 Proxy；
5、组件实例初始化速度提高 100%;
6、提速一倍/内存使用降低一半；

创建框架:npm init vite-app 项目名

当使用vue3写HTML时提示必须写在一个根标签中，只用在设置中搜eslint:将vetur不勾选

setup(){}:一个在vue生命周期beforeCreate之前调用的函数，可以来定义变量和方法，在模板中要使用，必须要return一个对象出来
要想在setup中使用父传子的属性要想在子代中接收，然后在setup函数中添加一个参数:Props，props就是父传子中的对象
{
    setup()函数中的参数:[
        1.props:就是在vue中定义的props父传子接收参数的对象，要在该组件中写了才可以调用，可以在setup函数通过props来访问父向子传递的参数
        2.context:可以获取到上下文，跟实例不一样
        {
            也可以取context中某一些属性
            用法:[
                {emit,attrs,slot} 来代替context对象，{}:在js中的语法为将对象进行展开，但是在vue中通过{}方式展开后就没有响应式，所有一般只通过{}来获取emit，其他的属性直接获取context对象来进行查看
                使用emit自定义事件，要先在vue实例中进行注册
                emit:["监听定义的事件名"]
            ]
        }
    ]
}

props:{
    还是定义在setup外面，在props中值可以在template模板中直接使用
}

以下是vue中新增的方法，使用先通过vue进行调用:import {ref,reactive,computed} from "vue"
**reactive**:{
    作用:对复杂数据类型进行响应式绑定
    语法:let 变量名 = reactive(值)
    调用:{
        js中:通过对象.属性名
        HTML中:通过对象.属性名
    }
    要在setup函数中要return出去
}
**watch**:{
    <!-- watch是不能监听非响应式变量 -->
    作用:监听变量变化
    语法:watch(变量,(a)=>{});监听变量a
    使用:watch(()=>{
        return props.title(变量名) || 但该变量被ref监听可以不用return直接使用变量，还不用.value,而reactive进行监听的变量不能这么使用
    },(newValue，oldValue)=>{
        console.log(newValue)
    })
    拓展:{
        可以同时监听多个变量:{
            在watch第一个参数中使用数组进行定义
        }
        响应函数:{
            响应函数中的参数当监听多个变量时，响应函数中的两个参数也是数组形式，数组中的值的顺序跟定义时的变量的位置一样
        }
        跟watchEffect监听函数一样也有句柄函数，及返回值也是一个函数，用来对watch进行停止的函数
        和callback回调函数，每当监听的值发生改变callback也会进行调用
    }
}
**computed**:{
    作用:计算属性
    语法:let 变量名 = computed(()=>{return})
    调用:{
        js中:通过变量名
        HTML中:直接使用变量名
    }
    要在setup函数中要return出去
}
**ref**:{
    作用:对基本数据类型进行响应式绑定
    语法:let 变量名 = ref(值),当你监听的变量为一个复杂数据类型时，内部还是通过reactive进行监听的
    调用:{
        js中:通过变量名.value
        HTML中:直接使用变量名
        reactive中:两者都可以----var c = ref(0); var obj = reactive(c)==reactive(c:c) == reactive(c:c.value)
    }
    要在setup函数中要return出去
}
**toRefs**:{
    作用:将reactive中的对象的逐个属性展开，转化为通ref函数绑定的变量
    语法:将reactive监听的对象改变为ref监听的变量，然后可以通过...将ref监听的变量中的所有属性展开，展开的属性依然是被监听的，但是在reactive中展开后不会被监听，所以toRefs一般这么用...toRefs(对象名),在return导出时使用
    调用:{
        js中:通过变量名.value
        HTML中:直接使用变量名
        setup:中还是要通过对象.属性名
    }
}
**isRef**(变量):判断该变量是否被ref进行监听
**isReactive**(变量):判断该变量是否由reactive监听
**isProxy**(变量):判断该变量是否由reactive或者readonly监听
**isReadonly**(变量):判断该变量是否由readonly监听
<!-- 有一个小的BUG，当const a = reactive({}) const b = readonly(a) 此时的b:isReactive(b)->true,isProxy(b)->true,isReadonly(b)->true -->
**unref**(变量):返回该变量的数据，相当于:isRef(a)?a.value:a == unref(a)
**toRef**(对象,属性名):返回将该属性名转化为一个被ref()监听的变量，在原来对象中还是存在并且无论通过对象或者变量对该属性值进行改变两边都会进行改变
**customRef**:{
    作用:该函数也被定义成一个监听对象，使用该监听的对象的对象改变有一个延迟的效果
    定义:function fn(value,delay=500){
        let t = null;
        return customRef((track,trigger)=>{
            return{
                get(){
                    track();
                    return value;
                },
                set(newValue){
                    clearTimeout(t)
                    t = setTimeout(()=>{
                        value = newValue;
                        trigger()
                    },delay)
                }
            }
        })
    }
    使用:const text = fn("a",100):然后return出去
}
**shallowRef**({}):用来监听变量，修改变量的值有可能不会发生响应式的变化,是一个浅拷贝,只能执行浅响应式，要使用triggerRef(变量名):来手动触发监听
**shallowReactive**({}):用来监听变量，修改变量的值有可能不会发生响应式的变化,是一个浅拷贝,只能执行浅响应式，要使用triggerRef(变量名):来手动触发监听
**shallowReadonly**({}):用来监听变量，修改变量的值有可能不会发生响应式的变化,是一个浅拷贝,只能执行浅响应式，要使用triggerRef(变量名):来手动触发监听
**toRaw**(变量):将响应式变量改变为普通变量，但是此时返回的变量还是跟响应式变量的地址相同，只是不具有响应式
**MarkRaw**(变量):使用markRaw()封装成普通变量是不能通过reactive等方法变为响应式对象
**watchEffets**:{
    作用:对数据进行监听，跟watch差不多
    语法:watchEffets(()=>{
        console.log(变量名)
    });
    区别:在定义时就会执行里面的函数，与watch监听函数不同的是，watch在定义时不会被执行一次
    返回值:一个函数当执行这个函数时，就不会进行监听了
    参数:oninvalidate:一个函数，可以在watchEffect中调用这个函数，该函数要定义一个参数--->一个可执行函数，每当监听的数据发生改变或者该watchEffect被销毁时都会调用，并且该函数的优先级最大，及最先调用
}
useRouter
useRoute
useVuex
这三个要从外部引入:然后在setup中执行该函数获取该实例化然后在进行操作

生命周期的hooks
声明周期:{
    beforeCteate-->setup
    created--->setup
    beforeMount--->onbeforeMount
    Mounted--->onmounted
    beforeUpdate--->onBeforeUpdate
    Updated--->onupdated
    beforeDestroy--->onBeforeUnmount
    destroued--->onUnmounted
}
vue3中的生命周期函数必须要从vue先导入，然后在写在setup函数中

getCurrentInstance:得到当前的实例
要从vue中导入
使用:{
    在setup(){
        const instance = getCurrentInstance();
        导入instance这个实例
        也可以只导入某一些参数
        const {ctx} = getCurrentInstance();//这个只能在开发环境下获取到this
        const {proxy} = getCurrentInstance()://这个在开发和生产环境下都有效
        跟setup中的ctx不同是ctx只能获取一些this上的参数，不是该模板的实例，而通过getcurrentinstance获取到的ctx|proxy就是当前实例
        一般使用proxy来获取到当前的实例，可以通过proxy来调用在全局vue中的定义的变量和函数
    }
}
定义全局变量和函数:{
    通过createApp();返回一个app实例化对象
    在app中有一个config属性，然后在config属性还有一个globalProperties对象，然后在该对象中定义变量或者函数
    app.config.globalProperties.a = "djsklfjk"
}

<!-- 使用optionAPI -->
后代传值api:{
    不需要导入，直接使用option api直接在该实例中定义
    把要传递的值写在provide中
    在后代中使用inject来接收该变量
    provide:{
        对象或者函数，
        使用:{
            1.对象:{
                name:"侯向毅"
                <!-- 在对象中不能使用thi对象 -->
            }
            2.函数:(){
                return {
                    name:this.name
                    <!-- 在函数的return中可以使用this -->
                }
            }
        }
    }
    inject:{
        数组
        ["name"]:在provide中的定义的变量名，要加引号
    }
}
使用composition api
<!-- 在vue中进行导入provide和inject -->
provide:{
    在setup中进行定义:{
        provide(name,key):一个provide定义一个变量和值，可以在setup中定义多个变量，
        要让该name变为响应式，其中key要使用ref进行监听，
        还可以通过provide来向后代传递方法，然后在后代进行调用
        当使用readonly对key进行监听时，该name值就不会在后代中被修改，但是可以通过provide传递方法然后进行修改
    }
}
inject:{
    <!-- 也可以使用option api方式进行接收 -->
    使用composition api方式进行接收
    在setup中进行定义:{
        const a = inject(name,default):name为在provide中传递变量的名字，default可以用来设置默认值，可以不写
        最后还是要return出去
    }
}

自定义指令:{
    directives:{
        1.首先定义一个对象:{}
        2.在对象中可以调用vue的所有生命周期hook，但是常用mounted，updated
        3.在对象中调用hook函数:{
            mounted(el,binding){
                el:使用该指令的标签对象
                binding:value属性就是你在指令中的定义的变量
            }
            updated(el,binding){
                el:使用该指令的标签对象
                binding:oldvalue:在数据没改之前的值，value数据发生改变后的值
            }
        }
    },
    定义完成后要在组件中的directives属性进行注册然后就通过v-指令进行调用
    如定义一个自动聚焦:
    const focus = {
        mounted(el){
            el.focus();
        }
    }
}

自定义全局组件:{
    app.component(组件名,组件实例)
}
定义一个文件导出一个对象在对象中定义一个install函数:{
    参数:app,option
}

app.use(name,options):{
    第一个参数为你要注册的插件名
    options:可以进行参数传递
}


vue-router使用:{
    1.下载:npm i vue-router@next
    2.创建一个rotuer.js文件:import { createRouter, createWebHashHistory,createWebHistory } from "vue-router":{
        1.createRouter({}):来创建router实例化对象
        2.routes:还是一样的配置
        3.history:选择模式=>createWebHashHistory:hash路由，createWebHistory:普通路由
    }
}

axios:{
    npm i axios --save
    --save:运行时依赖
    --save-dev:开发时依赖
    常用配置项:[
        1.url
        2.methods
        3.params:get请求时添加
        4.data:post请求时添加
        5.headers
        6.timeout
    ]
    常用方法:{
        1.all()
        2.interceptors:{
            response.use(function(config){}):响应拦截器,对返回的数据进行修改，最后return出去
            request.use(function(config){}):请求拦截器,对请求参数进行修改,最后要return出去
        }
        3.create({}):创建一个新的axios实例化对象
    }
}

router:[
    npm i router@next --save
    --save:运行时依赖
    --save-dev:开发时依赖
    常用配置项:[
        1.history
        2.routes
        3.isActiveClass
        4.base:根路径，一般不需要设置
    ]
    常用方法:{
        1.all()
        2.interceptors:{
            response.use(function(config){}):响应拦截器,对返回的数据进行修改，最后return出去
            request.use(function(config){}):请求拦截器,对请求参数进行修改,最后要return出去
        }
        3.create({}):创建一个新的axios实例化对象
    }
]

better-scroll:{
    常用配置项:{
        1.click:false|true,是否让在scroll中的标签进行点击事件的监听，默认为false
        2.probeType:[0|1|2|3],监听滚动的位置选择3就好了
        3.pullUpLoad:false|true,是否监听到下滑到底部和上拉到顶部,只会监听一次，监听完毕后需要调用再次开启的函数
        4.pullup:false|true,是否上拉刷新
        5.pulldown:false|true,是否下拉加载
        <!-- 3为4,5的综合写法 -->
    }
    常用函数:{
        1.finishPullUp():让scroll继续对下拉或者上拉进行监听
        2.scrollTo(x,y,delay):进行跳转到指定的位置，delay延迟，默认毫秒
        3.refresh():重新对DOM进行一次检查，当子标签中的高度发送改变时要重新进行一次计算
        4.on("",function(){}):对事件进行监听
    }
    常用事件:{
        1.scroll,{position}:当滚动时触发,position:{x,y}滚动的横纵位置
        2.pullingUp,无参:当下拉时触发
        3.pullingDown,无参:当上拉时触发
    }
}

