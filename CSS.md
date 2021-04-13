<!-- 文本属性 -->
文本属性{
    text-align:文本居中，
    text-decoration:下划线[none|underline|overline|line-through]
    text-indent:缩进[px|em]
    line-height:行高[px|%:百分比是相对于字体大小]
}
<!-- 字体属性 -->
字体属性:{
    font-size:字体大小[px|em|%]
    font-family:字体样式[雅黑|宋体]
    font-weight:字体粗细[bold|数字]
    font-style:字体风格[normal|italic:斜体|oblique]
    font-variant:字体变形[normal|small-caps:小写转为大写]
}
<!-- 背景 -->
背景:{
    background-color:背景颜色,包括的边框的大小进行填充颜色
    background-image:背景图片[url()],从padding开始进行填充图片，填充到下边框的位置
    background-origin:padding-box|border-box|content-box,设置背景颜色|背景图的起始原点，都填充到下边框的位置，默认为padding-box
    background-clip:padding-box|border-box|content-box,设置背景颜色|背景图的结束点，填充到设置的位置，默认为border-box
    background-size:cover|contain|100px 100px|100% 80%,背景图片的大小，cover相对于短长度全在盒子内，contain长的一段在盒子的内部
    background-repeat:背景叠加[no-repeat|repeat|repeat-x|repeat-y]
    background-position:背景位置[px|%|center|left]:先x后y，当没有定义Y的位置时默认为居中，方位名词可以混合使用
    background-attachment:背景固定[scroll|fixed]
    <!-- 渐变 -->
    通过background-image来设置
    1.线性渐变:linear-gradient(){
        第一个参数.to top:从下到上|to bottom:从上到下|to left:从右到左|to right:从左到右|还可以写角度12deg
        第二个参数.color 10%，可以写多个颜色，最少两个颜色，表示为该颜色占好多的比例，如果没写长度就平分长度
    }
    2.径向渐变:radial-gradient(){
        第一个参数.to top:从下到上|to bottom:从上到下|to left:从右到左|to right:从左到右|还可以写角度12deg
        第二个参数.color 10%，可以写多个颜色，最少两个颜色，表示为该颜色占好多的比例，如果没写长度就平分长度
    }
    2.重复线性渐变:repear-linear-gradient(){
        第一个参数.to top:从下到上|to bottom:从上到下|to left:从右到左|to right:从左到右|还可以写角度12deg
        第二个参数.color 10%，可以写多个颜色，最少两个颜色，表示为该颜色占好多的比例，如果没写长度就平分长度
    }
}
边框背景图片:{
    border-image:url();只在边框上显示图片
    border-image-slice:30:从上到下切割的范围 30:从右到左切割的范围 30:从下到上切割的范围 30::从左到右切割的范围
    border-image-repeat:repeat:重复填充图片全部填充|round:重复填充平均分布|
    border-image-width:图片可视化宽度
}
<!-- 阴影 -->
阴影:{
    box-shadow:盒子阴影{
        x:x轴位置，可以为负
        y:Y轴位置，可以为负
        blur:模糊程度，一个渐变效果
        spread:阴影大小，扩散
        color:阴影颜色
        inset:内阴影还是外阴影:默认为外阴影，inset为内阴影
    }
    text-shadow:文字阴影{
        x:x轴位置，可以为负
        y:Y轴位置，可以为负
        blur:模糊程度
        color:阴影颜色
    }
}
<!-- 浮动 -->
浮动:{
    脱标:脱离标准流,
    设置float属性
    去除浮动:{
        1.设置属性为clear:both
        2.伪类清除:content:"",display:block,clear:both;
        3.使用BFC
    }
}
<!-- BFC -->
BFC(block formatting Context)格式化上下文:{
    触发BFC模式:{
        position:absolute|fixed
        display:inline-block|table-cell|flex|inline-flex
        overflow:不为visible
        float:属性不为none
    }
    BFC模式的特性:{
        1.内部的Box会在垂直方向上一个接一个的放置:都有这个属性
        2.垂直方向上的距离由margin决定:外边距合并
        3.bfc的区域不会与float的元素区域重叠。
        4.计算bfc的高度时，浮动元素也参与计算
        5.bfc就是页面上的一个独立容器，容器里面的子元素不会影响外面元素。
    }
}
<!-- 居中 -->
居中{
    标准流:{
        水平:{
            margin:auto
        }
        竖直[只适用于文字居中]:{
            display:table-cell:表格盒模式
            vertical-align: middle;实现文字居中
        }
    }
    非标准流:{
        定位盒模型:{
            水平:left:50%;margin-left:-w/2
            水平:left:50%;transform:translateX(-50%)
            垂直:top:50%;margin-top:-h/2
            竖直:top:50%;transform:translateY(-50%)
        }
    }
}
<!-- 定位 -->
定位:{
    模式:{
        1.静态[默认]:static
        2.相对:relative
        <!-- 1,2的定位模式都不会脱离文档流 -->
        3.绝对:absolute
        4.固定:fixed
        <!-- 3,4会脱离文档流 -->
    }
}
<!-- vertical-align -->
vertical-align:实现文本竖直居中[middle|top|bottom|baseline]:{
    1.在display为inline-block就是行块盒模型
    2.在display中的table-cell就是表单盒模型
}
<!-- 图片空隙 -->
图片空隙:{
    1.产生原因:由于浏览器默认为图片与字体是基线对齐
    解决:{
        1.在图片中设置vertical-align:middle|bottom|top
        2.将display设置为block
        3.
    }
}
<!-- 文字溢出 -->
文字溢出:使用省略号代替{
    单行:{
        1.white-space:nowrap
        2.overflow:hidden
        3.text-overflow:ellipsis
    }
    多行:存在兼容问题{
        1.overflow:hidden
        2.text-overflow:ellipsis
        3.display:-webkit-box;
        4.-webkit-line-clamp:2
        5.-webkit-box-orient:vertical
    }
}
<!-- transition -->
transition:过渡{
    1.属性:设置触发的属性值[width|height|css中的属性|all:所有属性都满足]
    2.花费时间:
    3.运动曲线:[linear:匀速|ease:逐渐减慢|ease-in:加速|ease-out:减速|ease-in-out:先加后减]
    4.何时开始:
}
<!-- transform -->
transform:转换{
    translate:{
        平移
    }
    rotate:{
        旋转
    }
    scale:{
        缩放
    }
    transform-origin:旋转点
}
<!-- 动画animation -->
动画:{
    1.定义动画{
        @keyframes 动画名{
            0%{}
            100%{}
        }
    }
    2.动画的实现:{
        animation-name:动画名称
        animation-duration:持续时间
        animation-timing-function:动画运动曲线
        animation-delay:动画何时开始
        animation-iteration-count:播放次数[数字|infinite:一直播放]
        animation-direction:是否逆向播放[alternate:逆向播放|normal]
        animation-fill-mode:动画结束后是否回到起始位置[forwards:保持|backwards:回到]
    }
}
<!-- 3D -->
3D:{
    首先要添加在其父元素中添加一个透视的元素:perspective
    translate3d:{
        满足近大远小
    }
    rotate3d:{
        满足左手法则
        可以通过rotate3d(x,y,z,deg)
    }
    transform-style:{
        给子代开启3d环境
        preserve-3d:开启
        flat:默认为不开启
    }
}
<!-- flex布局 -->
flex:{
    justify-content:主轴的上盒子的分布[space-between|space-evely|space-around|center|flex-start]
    align-items:侧轴的上盒子的分布[flex-end|flex-start|center]
    flex-direction:重定向主轴的位置[column|row|column-reserve|row-reserve]
    flex-wrap:是否换行[no-warp|warp]
    align-content:当换行后来调整侧轴上盒子的分布
    flex-flow:flex-direction和flex-wrap的缩写
    定义在子类:{
        order:设置盒子的排列顺序，order值越小越在前面
        align-self:设置盒子在侧轴上的位置
    }
}
<!-- rem布局 -->
rem:{
    1.定义在HTML标签中的一个字体大小，在其后代标签中可以设置大小的为多少rem，就相当于设置rem为X，X的值在HTML中的font-size中
    2.使用media媒体查询:
    媒体查询的类别:{
        1.all用于所有的设备
        2.print用于打印机
        3.scree用于电脑，手机
    }
    媒体查询的关键字:{
        and:并且
        not:
        only
    }
    媒体特性:{

    }
    使用:@media scree and (max-width:800px):在屏幕上最大的宽度为800px，就显示为一下的css方案
    使用link标签引入:<link rel="stylesheet" href=".css" media="scree and (min-width:500px)">
}
<!-- 私有前缀 -->
私有前缀:{
    -o-:opera
    -webkit-:safari,chrome
    -ms-:ie
    -moz-:firefox
}
filter:[blur(数值):模糊处理]
cursor:鼠标样式[default|pointer|move|text|not-allowed]
visibility:隐藏或显示[hidden]
opacity:盒子的透明程度[0~1]
transparent:透明
text-align:可以让行块盒水平居中不一定是文字
pointer-events:none:不考虑该盒子
<!-- 自定义滚动条 -->
overflow-scrolling:touch{
    要先在其标签中添加这个属性
    **凹槽宽度**
    #scrollbar::-webkit-scrollbar{
    width:8px;
    height:8px;
    }
    **拖动条**
    #scrollbar::-webkit-scrollbar-thumb{
    background-color:ragb(0,0,0,0.3);
    border-radius:6px;
    }
    **背景槽**
    #scrollbar::-webkit-scrollbar-track{
    background-color:#ddd;
    border-radius:6px;
    }
}
权重:
    0级选择器:{
        *
    }
    1级选择器:{
        元素选择器: 元素标签
        伪元素选择器
    }
    2级选择器:{
        类选择器: .
        伪类选择器:
        属性选择器:
    }
    3级选择器:{
        id选择器: #
    }
    4级选择器:{
        写到元素的内部
    }
}
伪类选择器:{
    hover
    link
    active
    nth-child([数字|odd|even])
    first-child
    last-child
    nth-of-type([数字|odd|even])
    first-of-type
    last-of-type
    placeholder
    focus:具有焦点的标签
}
{
    nth-of-type与nth-child区别{
        nth-off-type:先把标签名跟nth前面一样先进行分组，分好在选(一定会渲染)
        nth-child:先找到满足的标签然后在看该标签是不是和nth前面的标签名一样(有可能不会进行渲染)
    }
}
属性选择器:{
    {
        [属性名称]:属性选择器，只要标签中有该属性名
        [属性名=属性值]:该属性名要相同并且属性值也要相同
        [属性名^=属性值]:该属性名相同并且属性值要以[]中的属性值开头
        [属性名$=属性值]:该属性名相同并且属性值要以[]中的属性值结尾
        [属性名*=属性值]:该属性名相同并且属性值要包含[]中的属性值
    }
}
一般选择器:{
    ' ':后代元素
    >:儿子元素
    +:兄弟元素
    after
    before
}

flex布局:{
    1.使用flex布局:对应失效的三个css属性:float,clear,vertical-align
    有一个order属性，定义在子标签中，表示一个权重，权重月越高就越靠后
}

column:{
    column-count:4:设置该标签中分为几栏布局
    column-rule:2px solid black:设置每一栏中间的分割线
    column-gap:2px:设置每栏之间的间隙
    column-span:all:表示为跨列
    column-fill:auto|balance:设置每一个栏的高度，auto自动，balance设置为最大的高度
}

chrome中特有属性:{
    -webkit-box-reflect:{
        box-reflect：包括3个值。
        1. direction 定义方向，取值包括 above 、 below 、 left 、 right。
            above：
            指定倒影在对象的上边
            below：
            指定倒影在对象的下边
            left：
            指定倒影在对象的左边
            right：
            指定倒影在对象的右边
        2. offset定义反射偏移的距离，取值包括数值或百分比，其中百分比根据对象的尺寸进行确定。默认为0。
        3. mask-box-image定义遮罩图像，该图像将覆盖投影区域。如果省略该参数值，则默认为无遮罩图像。
            取值：
            none：无遮罩图像：
            使用绝对或相对地址指定遮罩图像。
            使用线性渐变创建遮罩图像。
            使用径向(放射性)渐变创建遮罩图像。
            使用重复的线性渐变创建背遮罩像。
            使用重复的径向(放射性)渐变创建遮罩图像。
    }
}
mask:蒙层添加一个图片蒙层，让背景图片只显示蒙层中的
filter:滤镜:{
    none–默认值

    grayscale（value）–灰度，value:0~1;

    sepia（value）–褐色，value:0~1;

    saturate（value）–饱和度，value:number;

    hue-rotate（value）–色相旋转，value:angle;

    invert（value）–反色，value:0~1;

    opacity（value）–透明度，value:0~1;

    brightness（value）–亮度，value:0~1;

    contrast（value）–对比度，value:number;

    blur（value）–模糊，value:length;

    drop-shadow（value）–阴影value:h-shadowv-shadowblur
}