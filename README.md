# webpack 介绍
[原教学视频链接](https://www.youtube.com/watch?v=3On5Z0gjf4U)
## 此repo学习方法
* 每个commit为一个阶段的webpack应用修改
* 可以根据commit介绍，以及代码进行学习
* 以下为每个commit信息翻译

### Commits
1. 初始化应用，不包含webpack
    * 没有应用webpack之前的简单应用
    * app.js文件包含了所有代码
    * 通过CDS引用了Bootstrap,没有自定义样式或sass
    * 在assets文件夹包含一个SVG

2. 将代码分开到不同的脚本文件，不包含webpack
    * 将app.js分为5个脚本文件
    * 我们需要手动的将脚本引用到index.html
    * 我们还需要主要引用脚本的顺序
  
3. 安装webpack
    * 安装webpack和webpack-cli
    * 在package.json文件添加启动脚本(start script)
    * 新建一个index.js文件，这个文件是webpack默认识别的
    * webpack默认将代码输出到dist/main.js
    * 我们的代码暂时和webpack没有关系，但马上就会有了

4. 用webpack打包我们的代码
    * 我们用import/export来表明依赖
    * webpack会确保所有依赖会所需的顺序进行加载
    * 我们可以删除index.html中的全部脚本引用
  
5. 添加webpack配置文件
    * 新建webpack.config.js文件
    * 添加几个基本的配置
    * 修改package.json,以试webpack使用我们的配置文件

6. 添加loaders处理css
    * 安装 style-loader 和 css-loader
    * 添加配置让webpack应用这两个loader在ccs文件上 --> 添加 module.rules
    * 记住loaders在webpack.config中的顺序是需要注意的 --> use数组中提供的loaders将被倒序应用

7. 添加Sass loader,覆盖bootstrap颜色
    * 修改main.css为main.scss
    * 安装 bootstrap 以便我们操作
    * 安装 sass-loader 和 node-sass
    * 更新webpack.config文件添加一个.sass规则(rules)

8. 破坏缓存和 HtmlWebpackPlugin
    * 配置webpack在打包文件名中使用contentHash
    * 这导致index.html中没有脚本标签的问题
    * 安装 HtmlWebpackPlugin 来帮助我们生成新的index.html
    * 它将自动添加现有的脚本到文件底部
    * 我们创建一个模板文件template.html
    * 删除原先的index.html，因为我们不再需要了
    * 确保你打开dist/index.html来浏览应用

9. 添加prod(生产环境) 和 dev(开发环境) 配置，开发服务器(dev-server)
    * 将webpack.config文件复制3份
    * 分别为webpack.common.js, webpack.dev.js, webpack.prod.js
    * 安装webpack-merge来共享公共配置(common)
    * 更新package.json去使用新的配置文件
    * 安装webpack-dev-server添加到package.json中的启动脚本

10. 添加 html-loader, file-loader,和 clean-webpack-plugin
    * 添加html-loader自动require html中用到的图片资源
    * 添加file-loader来处理我们的 svg,png,jpg,gif 文件
    * 配置file-loader将我们的图像文件添加到dist/imgs文件夹
    * 同时配置给他们的文件们添加hash
    * 最后添加clean-webpack-plugin到我们的生产环境配置，在每次重建时将dist文件夹清空 

11. 为第三方库添加入口，添加bootstrap.js
    * 现在我们有两个入口(main, vendor)和两个打包文件(bubdle)
    * vendor文件将是放不经常改变的第三方库的
    * main文件包含我们自己的代码
  
12. 生产环境中打包JS, CSS, HTML
    * 生产时将CSS剥离到自己的文件中
    * 打包压缩CSS
    * 再次添加 TerserJS 用来压缩JS --> webpack默认是用Terser打包js文件的，当我在打包css配置minimizer后默认的方案将被覆盖，所以这里需要再次添加
    * 用HtmlWebpackPlugin来压缩HTML
