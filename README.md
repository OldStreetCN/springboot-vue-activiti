
# 前言

<font color=#999AAA > 目前市场上有很多开源平台没有整合工作流，即使有，也是价格不菲的商业版，来看这篇文章的估计也了解了行情，肯定不便宜。我这个快速开发平台在系统基础功能（用户管理，部门管理…）上整合了工作流，你可以直接用来开发ERP，OA，CRM等企业级应用，不用再担心如何再去花大量的时间集成工作流进来。博主是个人开发者。研究工作流有几年了，依稀记得第一次写工作流是用在江苏某省局的用车申请业务上，那时候年轻气盛，精力充沛可是能力有限，熬了几十个夜整出来了，即使出来了，也是代码很乱。后面也在好几个系统参与了工作流的开发，目前是单独把这一套给抽取出来了，做成了可插拔的，可以非常方便的整合到你的程序中。下面我们来探索吧。</font>



# 一、项目形式


springboot+vue+activiti集成了activiti在线编辑器，快速开发平台，可插拔工作流服务。

# 二、项目介绍


本项目拥有用户管理，部门管理，代码生成，系统监管，报表，大屏展示，业务审批等功能。功能太强大，只能粗矿的介绍，所见即所得，体验一下吧。


# 三、工作流
## 1.流程模型绘制
进入流程模型菜单，创建流程模型，这里涉及到网关流转，需要设置流转条件，我们这里是三十岁以上的走下面分支，三十岁以下的走上面的分支。点击分支线，设置流转条件即可。${age<=30}。保存后我们在列表中点击发布即可。
![绘制流程](https://upload-images.jianshu.io/upload_images/11416921-579a63188f917f9e?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![设置流转条件](https://upload-images.jianshu.io/upload_images/11416921-57634ba8a81e97b0?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11416921-72f1b98713a68a59?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



## 2.流程配置

发布后，就到了已发布模型列表，在启用之前，我们需要先对进行节点设置和关联具体单据。

![已发布模型](https://upload-images.jianshu.io/upload_images/11416921-9d50af5ff5fc6e4c?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<font color=#999AAA >审批人员可以根据角色，直接指定人，部门，部门负责人，发起人部门负责人来进行配置，基本上满足所有的流转需求，并且可以设置表单变量。

![节点设置](https://upload-images.jianshu.io/upload_images/11416921-20fe51a2690c258c?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<font color=#999AAA >设置流程表单，目前就做了一个请假的测试表单，并且可以对相应角色授权，做到自定义权限。
![设置关联表单](https://upload-images.jianshu.io/upload_images/11416921-bed7bccf884908bc?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<font color=#999AAA >设置完后启动即可。


## 3.流程提交
填写请假表单
![填写表单发起申请](https://upload-images.jianshu.io/upload_images/11416921-4cb6489b7d89e52d?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![列表](https://upload-images.jianshu.io/upload_images/11416921-14e733e02e4b32ff?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

提交单据，优先级分为普通，重要，紧急。消息通知可以选择站内通知，短信，邮件。

![提交表单](https://upload-images.jianshu.io/upload_images/11416921-8b5a1737596b3bba?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

提交之后可以撤回单据。
![撤回](https://upload-images.jianshu.io/upload_images/11416921-2aa0cbf83c4dd04a?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
<font color=#999AAA >查看流程流转进度情况。

![查看流转进度](https://upload-images.jianshu.io/upload_images/11416921-03afd146db7b241c?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

也可以挂起，删除流程。
![挂起](https://upload-images.jianshu.io/upload_images/11416921-acd8ab72ac9fcce4?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 4.流程审批
办理人审批列表，可以处理单据（驳回或者通过），也可以委托他们待办。
![审批待办](https://upload-images.jianshu.io/upload_images/11416921-0b2433f4342f0d1e?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
审批通过。
![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11416921-18d7f574e8afaba6?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
委托他们待办。
![委托他人待办](https://upload-images.jianshu.io/upload_images/11416921-05a4e0170ae3a241?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

审批通过后进入已办列表。
![已办列表](https://upload-images.jianshu.io/upload_images/11416921-0970eb13e2584ac3?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
年龄大于30岁，进入下面分支流转。
![流程查看](https://upload-images.jianshu.io/upload_images/11416921-2122efcc25bfb74c?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

审批通过。

![审批通过](https://upload-images.jianshu.io/upload_images/11416921-c17fffbeddf64c33?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 5.待办信息推送
站内消息推送。
![在这里插入图片描述](https://upload-images.jianshu.io/upload_images/11416921-abe4f33c22e3daa9?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)





# 总结
之前由于没有时间去部署线上测试环境，考虑近期部署，目前可以单独找我，远程演示，后面会逐步加强本系统其他功能，有需要的联系我。q:2500564056。

**鸣谢：**
jeecgboot开源版http://jeecg.com/
咖啡兔activiti实战https://kafeitu.me/
