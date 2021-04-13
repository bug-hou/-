使用命令webpack 加要打包文件的路径 打包到某处的路径

<!-- 设置webpack的配置文件 -->
1.在该文件夹下创建一个webpack.config.js文件
    webpack.js:{
        先要导入path,const path = require("path");
        创建一个module.exports对象
            在module.exports对象中
                entry：要打包的入口文件
                output:{将打包好的文件存放的地址
                    path:path.resolve(__dirname,"dist"),//将打包好文件存放在什么文件夹下面,注意要使用绝对路径
                    filename:"main.js",//将打包好的文件夹的文件的命字
                }
            }
    }
2.在该文件下通过npm init来创建package.json来记录下载的一些插件
package.json:{
    scripts:映射片段，在这里面可以书写一些代码进行映射，npm run 映射片段
    devDependencies:开发时依赖，通过npm install 插件@版本 --save-dev 可以不用加版本
}