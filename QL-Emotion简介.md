# 1. QL-Emotion简介

- QL-Emotion是基于SpringBoot+Mybatis开发的青龙面板管理系统
- API开发基于青龙面板 V2.10.13   YYDS版本进行开发

# 2. QL-Emotion的优势

- 同时管理多个青龙面板
- 不再担心青龙面板白屏
- 用户管理系统
- 动态羊毛中心
- 人性化的用户界面
- Android端呆瓜中心
- QQ机器人

# 3. 开始使用QL-Emotion

## 3.1 环境准备

-  一台服务器 (2h2g) 请不要同青龙部署在一个服务器上 青龙跑任务时占用内存比较大
-  宝塔面板 可视化界面 通俗易懂 (下面给出相应服务器的安装命令)
  - CentOs                    yum install -y wget && wget -O install.sh http://download.bt.cn/install/install_6.0.sh && sh install.sh
  - Ubuntu/Deepin        wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && sudo bash install.sh
  - Debian                     wget -O install.sh http://download.bt.cn/install/install-ubuntu_6.0.sh && bash install.sh
  - Fedora                     wget -O install.sh http://download.bt.cn/install/install_6.0.sh && bash install.sh

- Java 环境 

  -  通过宝塔面板的软件商店 搜索 java项目一键部署并安装 安装后点击设置找到 容器管理 选择tomcat8 安装后 java环境会自动配置

    

- 数据库Mysql
  -  宝塔面板软件商店搜索mysql 安装 mysql 5.6版本即可

## 3.2 修改QL-Emotion.jar

​	相关操作请观看视频教程

# 4.  开放API

## 4.1 用户API

- 用户登录  请求方式  POST

  ```json
  http://127.0.0.1:8080/open/login
  
  提交参数:{
      	"userName": "用户账号",
      	"userPsw": "用户密码"
  	}
  
  返回参数:
  	成功: { 
          	code: 0, 
          	data: token
           }
  	失败: {
          	code: 404,
          	message: "账号或密码错误"
      	 }
  ```

  

- 用户注册 请求方式 POST

  ```js
  http://127.0.0.1:8080/open/register
  
  提交参数: {
      	"userName": "用户登录账号",
  		"userPsw": "用户登录密码",
           "userQQ": "用户QQ",
           "userQuestion": "用户找回密码所需问题",
           "userAnswer": "问题答案"
  	}
  
  返回参数:
  	成功: { 
          	code: 0, 
          	data: "注册成功"
           }
  
  	失败: {
          	code: 404,
          	message: "暂未开放注册 请联系管理员"
      	 }
  
  	失败: {
          	code: 404,
          	message: "用户名已存在"
      	 }
  
  	失败: {
          	code: 404,
          	message: "注册失败"
      	 }
  ```

  

## 4.2 提交API

- 提交CK  提交方式 POST

  ```js
  http://127.0.0.1:8080/open/addJDVariable
  
      提交参数: {
              "qq": "用户qq",
              "ck": "cookie",
              "id": "容器ID",  可以为空 为空将会提交到剩余容量最多的容器 但必须有此字段
              "remarks": "用户备注",
              "token": token
          }
  
      返回参数:
          成功: { 
                  code: 0, 
                  data: "呆瓜成功"
               }
  	    成功: { 
                  code: 0, 
                  data: "更新成功"
               }
          成功: {
                  code: 0,
                  message: "您的账户已被禁用 请联系管理员"
               }
  
          成功: {
                  code: 0,
                  message: "CK无效"
               }
  
          失败: {
                  code: 404,
                  message: "青龙链接失败"
               }
  		失败: {
                  code: 404,
                  message: "容器已满"
               }
  		失败: {
                  code: 404,
                  message: "呆瓜失败"
               }
  		失败: {
                  code: 404,
                  message: "验证失败"
               }
  ```

  

- 提交其它羊毛  提交方式 POST  (注意 如果有则必须在网页端进行添加相关羊毛 才可呆瓜成功)

  ```js
  http://127.0.0.1:8080/open/addactivityVariable
  
  提交参数: {
              "vars": "羊毛名称", 例如 饿了么 美团 必须与羊毛中心添加的名称一致
              "ck": "cookie",
              "id": "容器ID",  可以为空 为空将会提交到剩余容量最多的容器 但必须有此字段
              "qq": "用户qq",
              "token": token    
          }
  
      返回参数:
          成功: { 
                  code: 0, 
                  data: "呆瓜成功"
               }
          成功: {
                  code: 0,
                  message: "您的账户已被禁用 请联系管理员"
               }
          失败: {
                  code: 404,
                  message: "青龙链接失败"
               }
  		失败: {
                  code: 404,
                  message: "容器已满"
               }
  		失败: {
                  code: 404,
                  message: "呆瓜失败"
               }
  		失败: {
                  code: 404,
                  message: "验证失败"
               }
  ```

  ## 4.3 查询API

  - 查询API  提交方式 GET 请在本地设置限次数查询  

    ```js
    http://127.0.0.1:8080/open/showUserIncome?qq=3117606283&token=
    
    返回参数
    		成功: { 
                    code: 0, 
                    data: userIncomeList   收入List数组
                 }
    		失败: {
                    code: 404,
                    message: "验证失败"
                 }
    ```

    

# 5 . 使用声明

- 二改造成的后果由二改人自行负责 均与 疯小瑞无关
- 整个系统 没有 任何上传变量的行为 若有 则为二次开发版本 请悉知
- 更多精彩 尽在 QQ群: 674895374  



