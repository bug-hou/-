promise:{
    理解:是JS中就进行异步处理编程的新的解决方案:{
        旧的方案:
        解决了回调地狱的问题
    }
    使用:new promise((resolve,reject)=>{
        异步操作代码
        然后调用resolve和reject函数
    })
}

promise:{
    状态:{
        进行中，成功|失败(成功和失败只能执行一个)
    }
}

promise->执行异步操作->成功了就执行resolve()|失败了就执行reject()->成功的回调函数定义在then中，参数一般使用value表示->失败的回调函数定义在catch中，参数用reason表示-->最后都是又可以为一个promise对象
异步函数的指向顺序:{先是settimeout,然后才是网络请求}
在promise的原型中内置了{
    .then:成功的回调函数
    .catch:失败的回调函数
    .all:可以同时实现多个promise对象参数为一个数组，放promise实例化对象，只有当所有的实例化对象都成功才可以调用then中的方法，否则调用catch并且只将第一个错误的返回进行调用,不能使用实例化进行调用，使用实例调用Promise.all([])
    .case:可以同时实现多个promise对象参数为一个数组，放promise实例化对象，只要有一个实例化对象成功就调用then中的方法并且只调用第一个返回的函数
}
在promise中也可以通过throw抛出一个异常从而调用reject失败的回调函数
throw:{
    使用:throw data
}
在promise中要定义回调函数，然后在promise实例化对象中对回调函数进行保存
在promise中定义了多个then函数都会被调用，但是只有第一个then中的value会被进行赋值，其他then中函数的参数为undefined，也就相当于在第一次回调函数进行return一个undefined参数，然后在后续的回调函数中对undefined参数进行接收进行调用调用回调函数，所有可以可以通过return 返回参数，就可以在后续的回调函数中对参数就进行定义
**在同一个promise中定义多个then的回调函数，这些函数都会进行调用，除了第一个选定的状态为失败时会调用失败的回调函数，后面的都会调用then的回调函数，并且可以同可以通过return来传递参数，如果没有传递参数，在下一个参数的值为undefined**

**当在promise中返回的是一个promise实例化对象，就不会只调用then的回调函数，还是要看return中promise的回调函数中的状态，从而选择回调函数**

**throw也可以该变调用的回调函数，当promise中出现throw会自动调用失败的回调函数，并且此时的状态变为失败，通过throw也可以进行参数传递，直接写throw后面**