https://www.iconfont.cn/:一个图表下载地址
http://bitbug.net/:网站图标转化网站
网站图标的引入:<link rel="shortcut icon" href="图标地址">
SEO优化:搜索引擎优化{
    title:一个标签，里面的内容时搜索引擎了解网页的入口，已经网页的划分归属
    description:写在meta标签中，网站说明
    keyword:写在mate标签中页面关键词
}

**在非BFC模式下margin-top会和进行合并**

块级元素:独占一行
行级元素:可以多个标签一起使用

块级元素：
h1~h6:标题的标签，当数字越大其主体大小越小
p:段落标签，用来表示为一个段落
hr:一条水平线，用来进行分割
br:换行标签

行块盒：
img:图片标签{
    title:当鼠标移动到图片中会出现的文字[该属性还可以用在其他标签中]
    src:图片链接
    alt:当图片未显示出来时用来alt中汉字代替
}
article:文章定义标签
aside:侧边定义标签

行标签:
a:瞄点标签，实现超链接{
    href:超链接的网站,也可以为某个网页的地址
}
abbr:缩写标签,实现将标签中的字下标有着重符号{
    title:当鼠标移动到图片中会出现的文字[该属性还可以用在其他标签中]
}
acronym:取首字母标签，实现将标签中的字下标有着重符号{
    title:当鼠标移动到图片中会出现的文字[该属性还可以用在其他标签中]
}

表格标签
table:一个表格{
    border:1边框属性，默认为0,
    align:该表在网页中水平上的位置[left|right]
    valign:该表中的纵向位置[top|bottom]
    cellspacing:设置该表中外边距的大小，默认为2
    cellpadding:内边距
}
tr:一行{
    table中
    align:该单元格在网页中水平上的位置[left|right]
    valign:该单元格中的纵向位置[top|bottom]
}
td:一个单元格{
    tr中
    align:该单元格在网页中水平上的位置[left|right]
    valign:该单元格中的纵向位置[top|bottom]
    colspan:合并水平方向上的单元格[数字]然后删除多余的单元格
    rowspan:纵行方向单元格的合并[数字]然后删除多余的单元格
}
th:头单元格{
    tr中
}
caption:标题标签，设置该表中的标题，为一个容器，在容器中可以写其他标签{
    table标签后面
}

input中type的属性{
    text:文本输入框，默认
    password:密码输入框，隐藏文本
    radio:单选框，当name相同是表示该几个单选框为一组
    checkbox:多选框，也是通过name来确定一组
    buttom:按钮
    submit:提交
    reset:重置
    image:图片按钮
    hidden:
    file:文件
    HTML5新增
    url:url字段
    email:邮箱字段
    color:颜色字段
    number:数字字段
    range:数值控件
    tel:电话
    month:年月控件
    date:日期空件
    datetime:日期加时间控件
}
input中其他属性:{
    required:表示该表单不能为空
    placeholder:提示信息
    autofocus:自动聚焦
    autocomplate:[off|on]
    checked:是否选中，一般只用在radio和CheckBox
}
textarea:文本域{
    resize:none
}
CSS选择器:{
    0级选择器:{
        *
    }
    1级选择器:{
        元素选择器: 元素标签
        ,:
        ' ':后代元素
        >:儿子元素
        +:兄弟元素
        [属性名称]:属性选择器，只要标签中包含有该属性名
        [属性名称=属性值]:属性选择器，属性名中的值跟等号后面的值相同
        [属性名称~=属性值]:标签中包含该属性名中有属性值的标签
        [属性名称|=属性值]:标签中以该属性名中有属性值开头的标签
        :hover:当鼠标悬浮到上面
        :focus:具有焦点的标签
        :nth-child(数字|odd(奇数)|even(偶数))
        :after:{
            content:"",
            display:inline-block
        }
        :first-letter:设置在该标签中第一个字符
        :first-line:设置该标签中第一行的样式
        selection:设置选中的文本的样式
    }
    2级选择器:{
        类选择器: .
    }
    3级选择器:{
        id选择器: #
    }
    4级选择器:{
        写到元素的内部
    }
}
vedio:视频播放{
    autoplay:自动播放
    controls:显示控件
    loop:循环播放
    preload:[auto|none]是否预习加载视频
    src:视频地址
    poster:加载等待的画面图片
    muted:静音播放
}
audio:视频播放{
    autoplay:自动播放
    controls:显示控件
    loop:循环播放
    preload:[auto|none]是否预习加载视频
    src:视频地址
    poster:加载等待的画面图片
    muted:静音播放
}
&nbsp;表示为空格
&gt;小于
&lt;大于