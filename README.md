<p align="center">
  <img src="logo.png" width="500px" height="350px" alt=" Logo">
</p>

### 👉 [Gewechat🤖](https://github.com/Devo919/Gewechat)，个人微信免费开源框架，支持二次开发、任意语言都可接入，Restful API接入。

#### 主要能力：
* 消息自动化、给指定对象（好友、群组）发送文本、图片、文件、emoji表情等消息
* 自定义消息处理、自动回复、文件下载、消息防撤回、各种自定义类型交互
* 群管理及好友管理、设置好友备注、邀请好友统计、拉好友进群等
* 各种业务模型接入，例如chatgpt、sora、大数据及客服模型
* 基于框架您可以创造更多有趣的功能...

<details><summary>免责声明【必读】</summary>

- 本框架仅供学习和技术研究使用，不得用于任何商业或非法行为，否则后果自负。

- 本框架的作者不对本工具的安全性、完整性、可靠性、有效性、正确性或适用性做任何明示或暗示的保证，也不对本工具的使用或滥用造成的任何直接或间接的损失、责任、索赔、要求或诉讼承担任何责任。

- 本框架的作者保留随时修改、更新、删除或终止本工具的权利，无需事先通知或承担任何义务。- 

- 本框架的使用者应遵守相关法律法规，尊重微信的版权和隐私，不得侵犯微信或其他第三方的合法权益，不得从事任何违法或不道德的行为。

- 本框架的使用者在下载、安装、运行或使用本工具时，即表示已阅读并同意本免责声明。如有异议，请立即停止使用本工具，并删除所有相关文件。

</details>

<details><summary>点击查看功能清单</summary>

- 获取登录二维码
- 执行登录
- 获取通讯录列表
- 获取通讯录列表缓存
- 获取群/好友简要信息
- 获取群/好友详细信息
- 搜索好友
- 添加联系人/同意添加好友
- 删除好友
- 设置好友仅聊天
- 设置好友备注
- 获取手机通讯录
- 上传手机通讯录
- 同步企微好友
- 获取企微好友详情
- 创建微信群
- 修改群名称
- 修改群备注
- 修改我在群内的昵称
- 邀请/添加 进群
- 删除群成员
- 退出群聊
- 解散群聊
- 获取群信息
- 获取群成员列表
- 获取群成员详情
- 获取群公告
- 设置群公告
- 同意进群
- 添加群成员为好友
- 获取群二维码
- 群保存到通讯录
- 管理员操作
- 聊天置顶
- 设置消息免打扰
- 扫码进群
- 确认进群申请
- 接收所有消息
- 下载图片
- 下载语音
- 下载视频
- 下载emoji
- cdn下载
- 发送文字消息
- 发送文件消息
- 发送图片消息
- 发送语音消息
- 发送视频消息
- 发送链接消息
- 发送名片消息
- 发送emoji消息
- 发送appmsg消息
- 发送小程序消息
- 转发文件
- 转发图片
- 转发视频
- 转发链接
- 转发小程序
- 撤回消息
- 添加标签
- 删除标签
- 标签列表
- 修改好友标签
- 获取个人资料
- 获取自己的二维码
- 获取设备记录
- 隐私设置
- 修改个人信息
- 修改头像
- 同步收藏夹
- 获取收藏夹内容
- 删除收藏夹
</details>



# 🚀 快速入门

#### 安装 (Centos Docker安装，已安装Docker可跳过)  


1、安装gcc相关
```
yum -y install gcc
yum -y install gcc-c++
```
2、配置镜像

```
yum install -y yum-utils
yum-config-manager --add-repo http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
yum makecache fast
```
3、安装docker

```
yum install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```


4、启动docker

```
systemctl start docker
//将docker设置成开机自启动
systemctl enable docker.service
```

#### 依赖库导入

1、导入镜像

```
 docker pull registry.cn-hangzhou.aliyuncs.com/gewe/gewe:latest
 
 docker tag registry.cn-hangzhou.aliyuncs.com/gewe/gewe gewe
```
2、运行镜像容器

```
mkdir -p /root/temp
docker run -itd -v /root/temp:/root/temp -p 2531:2531 -p 2532:2532 --privileged=true --name=gewe gewe /usr/sbin/init
```
3、将容器设置成开机运行

```
docker update --restart=always gewe
```
4、API服务调用

- [API文档]()

```
Api服务调用地址
http://ip+":2531/v2/api"  

文件下载地址
http://ip+":2532/download"
```

### 项目架构设计
 <img src="liucheng.jpg" width="600px" height="350px" alt=" Logo">


### 基本用法（java示例）
- 其他语言执行restful接口可实现相同功能，支持各类语言接入。
 
```
 //1、程序部署完成后先获取接口token
 JSONObject token = LoginApi.getToken();
 
 //2、token获取成功后将token值放入header即可访问api，每个api都需要校验token
 header.put("X-GEWE-TOKEN",token);
 
 /**
  *3、 获取登录二维码
  * @param appId   设备id 首次登录传空，后续登录传返回的appid
  * @param proxyIp 代理ip 格式：socks5://username:password@123.2.2.2:8932，同一区域可不传代理ip
  */
 JSONObject qr = LoginApi.getQr(appid, proxy);
 
 /**
  * 4、确认登陆
  * @param appId
  * @param proxyIp
  * @param uuid       取码返回的uuid
  * @param captchCode 登录验证码（跨省登录会出现此提示，使用同省代理ip能避免此问题，也能使账号更加稳定）
  */
  JSONObject jsonObject = LoginApi.checkQr(appId, proxyIp, uuid, captchCode);
  
  //5、第四步执行完成则表示微信已登录，执行下列类中的方法可实现不同功能
  LoginApi.class     //登录模块
  PersonalApi.class  //个人账号模块
  ContactApi.class   //联系人模块
  GroupApi.class     //微信群模块
  MessageApi.class   //消息模块
  LabelApi.class     //标签模块
  FavorApi.class     //收藏夹模块
```


### 注意事项：
- 1、由于容器需要用到 2531和2532端口，要保证服务器这两个端口没有被占用
- 2、容器启动后会访问腾讯服务器，因此要保证服务器能够访问外网，并且出网没有被限制，否则会导致容器无法正常启动


### 交流群：
<p align="center">
  <img src="mine.jpg" width="300px" height="300px" alt=" Logo">
</p>
<p align="center">
 添加好友备注GW加群交流
</p>



## 后续有新版本如何更新？
#### 更新流程

```
1、选择更新版本下载
2、将文件解压至服务器root目录
3、执行命令
    chmod +x install-gewe.sh
    ./install-gewe.sh

```


## 版本更新

### 1.0.0

* 正式1.0版本发布

<details><summary>点击查看更多</summary>

### 暂无

