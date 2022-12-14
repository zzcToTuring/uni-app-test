# uni-app-demo part
 
 之前使用原生的微信小程序代码开发过程序,但是在偶然之间发现了一个uni-app框架,按照他的说明,可以编译一次,在大多数场合运行,包括但云限制与iOS,Android,各类常见的小程序端

 特别的,他在vue框架的基础上进行运行,对有着一定vue基础的人来说应该会更加的好理解

 说的这么好听,在市面上有的资源+他的官方文档的作用下,我来尝试的学习一下uni-app这个框架

### 01_demo_uni-app

 这是一个空的创建,创建了一个基本的项目(或许在尝试做一些改变的时候修改了相关的代码)

 个人感觉这个框架有点抄,微信的原生小程序呢,在vue的基础上做了很多改进,感觉uni-app在别人的再次封装上再次做出了封装,emm我只能说我们是站在巨人的肩膀上进行吧

 其次,我以前都是用webstorm对前端项目进行开发的,但是看着他的官方文档中,并没有说明对其他编译器进行说明,只是说着之家编译器的使用方式,对一些开发者来说,这样的设定是不是有点不太友好呢?
 
 好像下载的指令也必须在HBuilder中进行使用,其他的编译器可能会出现无法预料的错误;编写完成之后只有HBuilder中直接点击进行运行......一系列的操作使得不得不在H中进行操作

#### uni-app的规范
 1 页面文件遵守vue单文件组件的规范
 2 组件表安静靠近小程序的规范
 3 接口能力(JS API)靠近微信小程序的规范,但需要将前缀WX替换成uni
 4 数据操作和事件绑定使用vue.js的规范,同时补充了APP及页面的生命周期
 5 为了兼容多端运行,建议使用flex布局进行开发

#### uni-app的心得
 使用过微信小程序开发都知道,原生的微信小程序开发将每个界面拆分成4个专门的界面,不用自己进行链接,只要在page中进行声明的,可直接链接

 在第一次使用uni-app框架时发现他的整体的布局长得特别像vue框架,他可以在h5界面使用也能在微信开发者工具中进行调试

 在微信开发者工具中进行调试就可以发现,他是把我们在uni-app中写的代码转化成了相关的微信开发的原生代码,同时,uni-app有着自己的官方文档,与微信的官方文档在有的地方有着出入,但是大体上相同,对程序的运行没有其他影响
 
 因此,在一些地方多阅读官方文档,能够更快的了解框架.同时,也能参考微信小程序的官方文档,毕竟是在他之上进行开发的框架

### hello-uni-app
 
 一个新的界面，上一个是一个空的项目，这个项目对一些简单的功能做了改变，但是实际上都大同小异，与微信原生的小程序差距不是很大

 tabBar配置项，与微信小程序的配置很相似，具体的配置如下--->简单的demo配置
 ```
 "tabBar": {
		"list": [
			{
				"pagePath": "pages/index/index",
				"text": "首页"
			},
			{
				"pagePath": "pages/message/index",
				"text": "信息"
			}
		]
	},
```

 condition配置，微信小程序的的编译方式，在这写明能在微信开发者工具中展示，起到更好调试的作用
```
"condition": {
		"current": 0,
		"list": [
			{
				"path": "pages/message/index",
				"query": "id=90",
				"name": "message页面编辑"
			}
		]
	}
```
 
 ###### 基础的配置项：
  
 与微信小程序相似的，uni-app框架也存在着一些基础的配置项；其中常见有类似于view，button，image属性，都能在官方文档中找到相关的解释

 ##### uni中的样式和less/scss样式

 原生的项目并不能直接编译less/scss这样的css预编译器，因此需要安装预编译插件，点击“工具”->插件安装，即可安装相关的插件，安装相应的插件能使用相关的预编译能力

 要是使用外联样式的话，可以使用外部导入，相关的代码如下说所示：
```
@import url("./a.css")
```

 ##### vue相关知识的学习
 
 本框架是基于vue相关技术,因此vue的相关学习是有必要的,但我已经开始看vue的源码了,这些东西都能跳过了吧

 ##### 与微信小程序类似的交互

 组件的生命周期,下拉,下拉,get请求和数据缓存,图片的上传与预览,都能通过官方的文档进行学习

 ### choice.vue界面

 在不同的环境中,我们可能会想要展示不同的内容,比如在微信小程序我想要一个按钮,在支付宝小程序我想要一个框,但我只想开发一次,这里就能使用到条件编译跨端兼容了

 语法:使用
 ```
 <!-- #ifdef H5 --> 
 <!-- #endif -->
 ``` 
 包裹住相关的代码

 ### 组件之间的跳转

 组件之间的跳转能够使用编程式和导航式两种方式,于小程序的开发类似

 其文档如下所示:https://uniapp.dcloud.net.cn/component/navigator.html

 编程式使用编程的形式,使用navigator组件包裹,示例的demo如下所示(open-type属性为打开方式,跳转到不同的位置有着不同的要求,具体参考官方文档)

 ```
 <navigator url="/pages/message/message" open-type="switchTab">跳转至信息页</navigator>
 
 <navigator url="/pages/detail/detail?id=80&age=19">跳转至详情页</navigator>
```
 同时也可以使用导航式的组件,及调用api的形式,跳转到不同的界面有着不同的api和不同的参数,以下是一些例子

```
goDetail () {
				uni.navigateTo({
					url: '/pages/detail/detail?id=80&age=19'
				})
			},
			goMessage () {
				uni.switchTab({
					url: '/pages/message/message'
				})
			},
			redirectDetail () {
				uni.redirectTo({
					url: '/pages/detail/detail'
				});
			},
			addToCar () {
				uni.$emit('updateCart',{
					id: 10,
					name: '贸易'
				})
			}
		}
```
 
 tip:同时也能携带一些参数,参数的读取可通过生命周期onload中的第一个参数读取

#### 组件的创建与使用&组件的生命周期
 
 不能说一模一样,只能说毫不相关吧,生命周期的话是和vue一模一样的,没有任何的区别

### 组件之间通信

 组件之间的通信方式有父传子,子传父,兄弟组件之间的通信

 父传子与子传父两者都是可以通过简单的props和提前传递相关的接口方式完成

 兄弟组件之间(vuex太过于复杂没有体现)使用的是类似于vue中的事件总线bus的方式完成相关的通信

 但与vue所有不同,在于他的相关api调用
```

<template>
	<view>
		这是a组件：<button @click="addNum">修改b组件的数据</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods: {
			addNum () {
				uni.$emit('updateNum',10)
			}
		}
	}
</script>

<style>

</style>


<template>
	<view>
		这是b组件的数据:{{num}}
	</view>
</template>

<script>
	export default {
		data() {
			return {
				num: 0
			};
		},
		created(){
			uni.$on('updateNum',num=>{
				this.num+=num
			})
		}
	}
</script>

<style>

</style>

```
 使用uni.$on与uni.$emit完成,与vue中的bus又点区别,变得更加简单了吧


 #### uni-ui组件库的使用

 在test/index.vue文件夹中,使用的是uni-UI组件库

 首先在https://uniapp.dcloud.net.cn/component/ 中选择扩展组件,选择使用的插件安装到本地(其实vue中的elementUI也需要安装,只不过是npm帮我们做了这一系列操作)

 按照他的文档进行操作

 以下是一个demo
```
<template>
	<view>
		 <uni-calendar 
		    :insert="true"
		    :lunar="true" 
		    :start-date="'2019-3-2'"
		    :end-date="'2019-5-20'"
		    @change="change"
		     />
	</view>
</template>

<script>
</script>

<style>
</style>
```

 其实为什么不用引入就能调用,我也不清楚,我看着他官方文档说的使用了什么什么技术因此不需要使用import

 要是需要使用import的话,与vue相似,导入注册展示

# part end

 上面的文档是uni-app的基础,感觉掌握了vue的话,过一下官方文档就能开始做开发了,基于vue框架上进行开发但是与vue又有一些不同,可能是考虑到要兼容其他平台的开发吧

 个人感觉,是使用vue和wx.api进行了一些合并,不过确实的,对会vue的开发者更加友好

 end----> 以后尝试着使用框架做一些开发吧,uni-app的基础部分就到此结束了(代码没什么参考,都是自己写的好乱的demo)
 

 


 



 



