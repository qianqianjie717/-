# 2022年夏季《移动软件开发》实验报告



<center>姓名：杨惠婷  学号：20020007091</center>

| 姓名和学号？         | 杨惠婷，200020007091                  |
| -------------------- | -------------------------------- |
| 本实验属于哪门课程？ | 中国海洋大学22夏《移动软件开发》 |
| 实验名称？           | 实验1：第一个微信小程序          |
| 博客地址？           | XXXXXXX                          |
| Github仓库地址？     | XXXXXXX                          |

（备注：将实验报告发布在博客、代码公开至 github 是 **加分项**，不是必须做的）



## **一、实验目标**

1、学习使用快速启动模板创建小程序的方法；
2、学习不使用模板手动创建小程序的方法。


## 二、实验步骤

列出实验的关键步骤、代码解析、截图。
###1.选择如下选项，即可快速创建启动模板创建小程序
![](1.png)
###2.按如下步骤完成手动创建
####得到1操作的模板，并删除模板上的各种元素（删除utils文件夹，logs文件夹，清空index.js，app.js和app.wxss的全部代码并创建原有函数）
####对默认导航栏的操作在app.json的window属性中进行
	 "window":{
    "backgroundTextStyle": "dark",
    "navigationBarBackgroundColor": "#ccffcc",
    "navigationBarTitleText": "第一个小程序",
    "navigationBarTextStyle": "black"
  },

####页面元素设计在index.wxml中完成（此时的头像，名称均为个人所起）
	<view class="container">
  	<image src='{{src}}' mode="heightFix"></image>
  	<text>{{name}}</text>
  	<button class="small" open-type="getUserInfo"bindtap="getMyInfo">
    	点击获取头像和昵称
  	</button>
	</view>
####index中元素的属性在wxss中定义
	.container{                         /*对container类的属性设置*/
  		height:100vh;
  		display: flex;
 		flex-direction: column;         /*垂直布局*/
  		align-items: center;            /*水平方向居中*/
  		justify-content: space-around;  /*垂直分散布局*/
	}
	image{
  		height: 300rpx;
  		border-radius: 0%;
	}
	text{
  		font-size: 50rpx;
	}
	.small{  
  		font-size: 30rpx                /*对small类的属性设置*/
	}
####实现button属性中的getMyInfo事件，获取用户信息
#####开发者需要获取用户的个人信息（头像、昵称、性别与地区），可以通过wx.getUserProfile接口进行获取，该接口中desc属性（声明获取用户个人信息后的用途）后续会展示在弹窗中
	getMyInfo:function(e){              /*此处对应bindtap绑定的事件名*/
    	wx.getUserProfile({
      		desc: '简单展示',
      		success:(res) => {          /*成功获取权限之后的操作*/
        		console.log(res)
        		this.setData({          /*修改头像昵称*/
          			src:res.userInfo.avatarUrl,
          			name:res.userInfo.nickName
        		})
      		}
    	})
	},
#####wx.getUserProfile获取用户信息。每次请求都会弹出授权窗口，用户同意后返回 userInfo
	onLoad(){
    	if(wx.getUserProfile){
      		this.setData({
        		canIUseGetUserProfile:true
      		})
    	}
	},
## 三、程序运行结果

列出程序的最终运行结果及截图。
![](2.png)
![](3.png)
![](4.png)

## 四、问题总结与体会

描述实验过程中所遇到的问题，以及是如何解决的。有哪些收获和体会，对于课程的安排有哪些建议。
###1.按钮的字体过大，想修改。通过对text内的属性修改，发现无效，故将按钮定义为一个类，使用同样大小的字体
###2.获取用户信息失败。微信期间对小程序开发进行过调整，新增了wx.getUserProfile接口用来获取用户信息，故在此使用此接口完成用户信息的获取以及显示