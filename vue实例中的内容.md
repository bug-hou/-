1.vnode:虚拟DOM{
    children.default()[0]:返回一个虚拟DOM，当该组件的儿子只有一个时，该虚拟DOM中的children为null，该虚拟DOM的信息保存在该对象中，当有多个儿子时，每个儿子的信息都保存在children一个数组中
    key:只有定义了key才可以访问到key值
    props:定义在该组件中的所有的值都在props对象中，包括class等类名
    <!-- 只是个人认为较重要的属性 -->
}
2.proxy:vue的实例化对象{}
3.ctx:vue的实例化对象:跟proxy一样{}
4.attrs:父代向子代传递的参数，并且该参数并未在props中接收
5.parent:获取到父代中的vue对象，vue对象包含的属性也有这些内容，一般用来获取父组件中的proxy属性也就是父组件的实例化对象，取定义在父组件的变量
6.slots:获取到该实例化中插槽中的对象{
    跟虚拟DOM中的children一样
}
<!-- 在模板中通过ref获取到vue实例化对象相当于vue对象中的ctx或者proxy -->
vue实例化对象:{
    $: (...)
    $attrs: (...)
    $data: (...)
    $el: (...)
    $emit: (...)
    $forceUpdate: (...)
    $nextTick: (...)
    $options: (...)
    $parent: (...)
    $props: (...)
    $refs: (...)
    $root: (...)
    $router: (...)
    $slots: (...)
    $watch: (...)
    props中的属性
    该实例return出来的属性和方法
    定义在全局的属性和方法
}