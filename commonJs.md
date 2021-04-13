commonJS中导入导出的语法:{
    导入:{
        const name = require(path):定义一个变量来接收导入路径的值
        <!-- require来获取到是该文件中导出的内容，require只能接收module.exports方式导出的文件，接收的为module.exports这个对象 -->
    }
    导出:{
        module.exports = name:将name这个变量导出
        <!-- module.exports相当于一个对象，每一个js文件中都可以定以一个,可以通过module.exports.a=name,module.exports.b=path来导出多个数据 -->
    }
}
<!-- commonJS是一个后端语言，及node.js，可以在本地运行，而JavaScript只能在服务器上运行 -->
<!-- 在vue中写vue文件时只能使用es6语法的导入导出 -->
<!-- 在配置vue.config.js文件时不是在页面上显示的要使用node.js语法来导入导出 -->
es6导入导出的语法:{
    导入:{
        import "path"
        import name from "path"
    }
    导出:{
        export let|const|var|class|function name?=():在导出时必须重新定义一个变量，可以导出多个变量，使用import接收时必须和导出变量名一样，并且要在import中加{}
        export default name?=():可以导出在文件之前定义好的变量,只能导出一次，可以把导出变量设置为一个对象，然后在对象导出多个
    }
}