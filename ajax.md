ajax:{
    1.先实例化对象: new XMLHttpRequest();
    2.对实例化对象进行初始化配置，设置请求方式和url: xhr.open(methods(请求方式),url(请求地址))
    {
        如果要设置请求头，或者请求行在open后面进行设置
        setRequestHeaders(key,value):用来设置请求头
    }
    3.发送:xhr.send(当有参数时可以将参数写在里面如:"a=100&b=200");
    4.事件绑定；处理服务端返回的结果{
        1.onreadystatechange{
            readystate:是xhr中对象属性,在xhr中使用数字作为状态码[0 xhr初始化,未open,1 执行发送动作,指向open,2 请求已经发送,3 数据正在解析,4 数据解析完成，可以使用了]
            change:改变
            这个事件表示为当状态码发送改变时调用
            只有当状态码为4时才会进行触发
        }
    }
    XMLHttpRequest实例化对象中包含，这些属性都是可以设置的:{
        onabort: **当请求被取消的回调函数**
        onerror: **网络异常的回调函数**
        onload: **当请求成功数据回来时的回调函数**
        onloadend: null
        onloadstart: null
        onprogress: null
        onreadystatechange: ƒ (e)**状态码改变事件**
        ontimeout: null**事件超时事件**
        readyState: 4**状态码**
        response: "HELLO EXPRESS"**响应体**
        responseText: "HELLO EXPRESS"**响应文本**
        responseType: ""**响应类型,当设置为json时可以将json返回的内容解析为对象**
        responseURL: "http://localhost:8000/server"**响应地址**
        responseXML: null
        status: 200**响应码**
        statusText: "OK"**响应状态字符串**
        timeout: 0**设置超时的时间**
        upload: XMLHttpRequestUpload {onloadstart: null, onprogress: null, onabort: null, onerror: null, onload: null, …}
        withCredentials: false
        abort():**用来取消请求的发送**
        getAllResponseHeaders():**得到响应头**
        setRequestHeader(key,value)**设置请求头**
    }
}
http:{
    1.HTTP:超文本传输协议:协议详细规定了浏览器和万维网服务器之间互相通信的规则
    2.请求报文:{
        1.请求行: GET(请求方式) / 请求内容 协议名(HTTP1.1和HTTP2.0)
        2.请求头:{
            1.Host: 请求的域名或者IP
            2.Cookie: 用来存放临时信息的
            3.Content-type:
            4.User-Agent: 简称UA:标明是什么浏览器发起的请求
            格式:**名字,冒号,空格,内容**如 Host: baidu.com
        }
        3.请求空行:就是一个空行
        4.请求体:用来写你请求时要发送的参数
    }
    3.响应报文:{
        1.行: 协议版本(HTTP1.1和HTTP2.0) 响应状态码(200) 响应状态字符串(OK,这个由响应状态码决定)
        2.头:{
            1.Content-type:text/html;charset=utf-8;
            2.Content-length:2048
            3.Content-encoding(压缩方式):gzip
        }
        3.空行
        4.体:就是请求后得到的东西，用户要的内容
    }
}
响应状态码:{
    200:成功
    301:重定向
    304:从缓存中获取
    401:未授权
    403:被禁止
    404:没有找到
    500:内部错误
    <!--  -->
    100~199:请求还在继续，服务器已经收到请求，正在处理该请求
    200~299:请求成功
    300~399:重定向
    400~499:客户端错误
    500~599:服务端错误
}

在发送请求时浏览器中的参数指示的标题:{
    get:query string params
    post:{
        <!-- 参数样式为普通样式:a=13&b=12... -->
        1.当content-type不指定参数并且参数url分离:text/plain;charset=utf-8,:request payload，该类型下参数格式为普通模式
        2.当content-type没指定并且参数与url为分离:query string parameters,这个跟get请求显示的一样
        3.当content-type指定为application/x-www-form-urlencoded:Request Payload，该类型下参数格式为普通模式
        3.当content-type指定为application/json:Request Payload，该类型下参数格式必须为json字符串，JSON.stringify():就是将json对象转化为json字符串
    }
}
同源与跨域{
    同源:{
        只有当协议，域名，端口全部一样才满足同源策略
    }
    跨域:{
        只要不满足同源策略就是跨域请求
        跨域请求的方式:{
            1.jsonp
            2.代理
            3.cors
        }
    }
}

协议:[
    http1.0每一次请求都是一个连接
    http1.1一次请求完毕以后,这个连接还不会立马消失,而是存活一段时间,这个时间大概是3秒
]
get与post的区别:{
    比较点 :  get            post
    url    :  可见           不可见
    安全   :  不安全         较安全
    参数   :  拼接到url中    通过请求体传递参数
    缓存   :  有缓存         无
    大小   :  url长度限制    理论上没有，但是IE有限制2kb
    作用   :  请求数据       传递数据
    速度   :  快             慢           
    <!-- 这点可能也就是为什么post请求这么好为什么不只使用post请求 -->
    为什么post较慢:{
        1.post的请求参数放在请求体中的，并且在请求体中可以使用不同类型参数的格式，所有会在请求头中设置content-type:请求体的参数类型
        这一点影响很小，在请求头中有更多的参数
        2.post会进行3次握手:{
            post请求的过程：
            （1）浏览器请求tcp连接（第一次握手）
            （2）服务器答应进行tcp连接（第二次握手）
            （3）浏览器确认，并发送post请求头（第三次握手，这个报文比较小，所以http会在此时进行第一次数据发送）
            （4）服务器返回100 Continue响应
            （5）浏览器发送数据
            （6）服务器返回200 OK响应
            get请求的过程：
            （1）浏览器请求tcp连接（第一次握手）
            （2）服务器答应进行tcp连接（第二次握手）
            （3）浏览器确认，并发送get请求头和数据（第三次握手，这个报文比较小，所以http会在此时进行第一次数据发送）
            （4）服务器返回200 OK响应
        }
    }
}