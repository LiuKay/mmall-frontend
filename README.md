# Mmall 前端工程

> Fork from [fenix-bookstore-frontend](https://github.com/fenixsoft/fenix-bookstore-frontend)

## 运行程序

以下几种途径，可以马上浏览最终的效果：

- 通过Git上的源码，以开发模式运行：
>```bash
># 克隆获取源码
> $ git clone https://github.com/LiuKay/mmall-frontend.git
>
> # 进入工程根目录
> $ cd mmall-frontend
>
> # 安装工程依赖
> $ npm install
>
> # 以开发模式运行，地址为localhost:8080
> $ npm run dev
> ```
>
> 然后在浏览器访问：[http://localhost:8080](http://localhost:8080)
>

```bash
# 编译前端代码
$ npm run build
```

或者使用--report参数，同时输出依赖分析报告：

```bash
# 编译前端代码并生成报告
$ npm run build --report
```

编译结果存放在/dist目录中，应将其拷贝至Web服务器的根目录使用。对于Fenix Project的各个服务端而言，则通常是拷贝到网关工程中静态资源目录下。

## 与后端联调

同样出于前后端分离的目的，理论上后端通常只应当依据约定的服务协议（接口定位、访问传输方式、参数及模型结构、服务水平协议等）提供服务，并以此为依据进行不依赖前端的独立测试，最终集成时使用的是编译后的前端产品。

不过，在开发期就进行的前后端联合在现今许多企业之中仍是主流形式，由一个人“全栈式”地开发某个功能时更是如此，因此，当要在开发模式中进行联调时，需要修改项目根目录下的main.js文件，使其**不**导入Mock.js，即如下代码所示的条件语句判断为假

```javascript
/**
 * 默认在开发模式中启用mock.js代替服务端请求
 * 如需要同时调试服务端，请修改此处判断条件
 */
// eslint-disable-next-line no-constant-condition
if (process.env.MOCK) {
  require('./api/mock')
}
```

也有其他一些相反的情况，需要在生产包中仍然继续使用Mock.js提供服务时（譬如Docker镜像icyfenix/bookstore:frontend就是如此），同样应修改该条件，使其结果为真，在开发模式依然导入了Mock.js即可。

## 工程结构

Mmall 的工程结构完全符合vue.js工程的典型习惯，事实上它在建立时就是通过vue-cli初始化的。此工程的结构与其中各个目录的作用主要如下所示：

```
+---build                           webpack编译配置，该目录的内容一般不做改动
+---config                          webpack编译配置，用户需改动的内容提取至此
+---dist                            编译输出结果存放的位置
+---markdown                        与项目无关，用于支持markdown的资源（如图片）
+---src
|   +---api                         本地与远程的API接口
|   |   +---local                   本地服务，如localStorage、加密等
|   |   +---mock                    远程API接口的Mock
|   |   |   \---json                Mock返回的数据
|   |   \---remote                  远程服务
|   +---assets                      资源文件，会被webpack哈希和压缩
|   +---components                  vue.js的组件目录，按照使用页面的结构放置
|   |   +---home
|   |   |   +---cart
|   |   |   +---detail
|   |   |   \---main
|   |   \---login
|   +---pages                       vue.js的视图目录，存放页面级组件
|   |   \---home
|   +---plugins                     vue.js的插件，如全局异常处理器
|   +---router                      vue-router路由配置
|   \---store                       vuex状态配置
|       \---modules                 vuex状态按名空间分隔存放
\---static                          静态资源，编译时原样打包，不会做哈希和压缩
```

## 组件
Mmall 前端部分基于以下开源组件和免费资源构建：

- [Vue.js](https://cn.vuejs.org/)<br/>
  渐进式JavaScript框架
- [Element](https://element.eleme.cn/#/zh-CN)<br/>
  一套为开发者、设计师和产品经理准备的基于Vue 2.0的桌面端组件库
- [Axios](https://github.com/axios/axios)<br/>
  Promise based HTTP client for the browser and node.js
- [Mock.js](http://mockjs.com/)<br/>
  生成随机数据，拦截 Ajax 请求
- [DesignEvo](https://www.designevo.com/cn)<br/>
  一款由PearlMountain有限公司设计研发的logo设计软件

## 协议

- 本文档代码部分采用[Apache 2.0协议](https://www.apache.org/licenses/LICENSE-2.0)进行许可。遵循许可的前提下，你可以自由地对代码进行修改，再发布，可以将代码用作商业用途。但要求你：
  - **署名**：在原有代码和衍生代码中，保留原作者署名及代码来源信息。
  - **保留许可证**：在原有代码和衍生代码中，保留Apache 2.0协议文件。

- 本作品文档部分采用[知识共享署名 4.0 国际许可协议](http://creativecommons.org/licenses/by/4.0/)进行许可。 遵循许可的前提下，你可以自由地共享，包括在任何媒介上以任何形式复制、发行本作品，亦可以自由地演绎、修改、转换或以本作品为基础进行二次创作。但要求你：
  - **署名**：应在使用本文档的全部或部分内容时候，注明原作者及来源信息。
  - **非商业性使用**：不得用于商业出版或其他任何带有商业性质的行为。如需商业使用，请联系作者。
  - **相同方式共享的条件**：在本文档基础上演绎、修改的作品，应当继续以知识共享署名 4.0国际许可协议进行许可。
