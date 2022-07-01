## **鲲鹏HTTP服务说明**

> 目前鲲鹏框架的50+的API都在下面写了，如果框架后续有更新，那么会继续添加。
*****
> API提交数据请使用POST提交JSON，请勿使用除了POST以外的其他方式提交数据，请在请求头设置content-type: application/json，否则无法通过。
以下API的返回都只是提供参考，具体还是看接口返回的数据，不过都将是返回JSON格式的数据。
*****
> WS已经更新，最新版本直接开启即可使用(自行看插件界面)
> WS推送和接口调用都是json格式，自己试试即可，和HTTP差不多。
*****
> 》鉴权计算方法《
第一步：将所有的值按照文档上的顺序拼接到一起
第二步：将拼接好的值放在中间，前面和后面各加上一个鉴权密钥
第三步：将上面拼接好的字符串(utf-8)用md5方式加密一次，取32位(大小写不敏感)
第四步：将使用md5加密后的字符串再次加密后，在待提交的json中加入sign字段一起提交到接口即可
~~~
示例(以初始化接口为例子)：
str = 鉴权KEY+K10001+软件唯一ID+软件名称+版本号+软件KEY+鉴权KEY
sign = md5(md5(str))
{
    "api": "K10001",
    "appId": "10001",
    "appName": "软件1",
    "appVer": "1.0",
    "appKey": "1668532261",
    "sign":sign
}
// 注意最好按照下面文档的顺序进行字符串的拼接
// 经过md5加密后的字符串再用md5加密一次即可
// 然后在最后加入到JSON的最后面(很重要)
~~~
*****
> **插件和Demo下载地址：[鲲鹏HTTP服务](https://www.123pan.com/s/esJDVv-sovq)**
PS：请注意识别正版，防止病毒等恶意文件。
*****
> 欢迎各位投稿自己会的语言的Demo，如：Java、python、PHP、GoLang等，投稿联系肥猫QQ1668532261
> **Demo提供者名单(排名是投稿先后顺序，技术不论，请勿过多解读)**
> **Python①：One (Q 1875874066) - [下载](https://www.123pan.com/s/esJDVv-jmvq)**
> **Python②：胡萝卜(Q 2605307210) - [下载](https://www.123pan.com/s/esJDVv-Vmvq)**
> **Python③：bhrs(Q 2484240274) - [下载](https://www.123pan.com/s/esJDVv-qmvq)**
> **Java①：肥猫(Q 1668532261) - [下载](https://www.123pan.com/s/esJDVv-ymvq)**
> **PHP①：WILL(Q 1852481) - [下载](https://www.123pan.com/s/esJDVv-11vq)**
> **C#①：老头(Q 123763753) - [下载](https://www.123pan.com/s/esJDVv-2avq)**
*****
> 温馨提示：消息推送请在插件填写好接收的API地址即可，推荐使用本地API，因为发送文件、图片等都是本地路径才可发送，后续可能有时间会更新填写网址也能发送。
PS：如果您愿意支持，可以在[鲲鹏HTTP服务]插件的设置窗口扫描二维码打赏一下，生活不易，肥猫叹气，为爱发电，我也乐意。
*****
>![](images/三大平台收款二维码.png)
*****
# **推送说明**
> 您只需要在插件界面填写好接收消息的网址即可，如：http://127.0.0.1:123/Msg
> 然后插件有任何消息都会推送JSON格式的数据到您的网址，POST提交方式。
> 格式请自行接收几个看看，框架原因无法给您解释JSON里面的东西是一些什么。
> 您在接收到JSON后，可以取出里面的数据调用下方API，如：收到私聊给您的机器人发送的消息，做出回应，调用下方接口，主动提交一个POST请求到接口即可
> PS：您如果是外网调用接口，请自行奖将127.0.0.1换成你服务器对应的IP地址。
*****
# **API接口**
### 初始化[K10001]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10001#API代码，必须有
*appId=10001#软件唯一id，暂时随意
*appName=软件1#软件名称
*appVer=1.0#软件版本号
*appKey=1668532261#软件Key，暂时随意
<<<
success
{
    "msg": "初始化成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "初始化失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 添加日志[K10002]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10002#API代码，必须有
*type=1#1调试，2警告，3提示
*msg#日志内容
<<<
success
{
    "msg": "添加日志成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "添加日志失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 关注公众号[K10003]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10003#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#公众号的wxid，勿填错
<<<
success
{
    "msg": "关注公众号成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "关注公众号失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 转账收款[K10004]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10004#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#群id，勿填错
*transferid#收到的转账transferid
<<<
success
{
    "msg": "转账收款成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "转账收款失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 转账退款[K10005]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10005#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#群id，勿填错
*transferid#收到的转账transferid
<<<
success
{
    "msg": "转账退款成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "转账退款失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 同意群聊邀请[K10006]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10006#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#群id，勿填错
*url#收到的消息里获取
<<<
success
{
    "msg": "同意群聊邀请成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "同意群聊邀请失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 消息免打扰[K10007]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10007#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*isFlag=1#是否免打扰，0/1
<<<
success
{
    "msg": "消息免打扰设置成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "消息免打扰设置失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 置顶聊天[K10008]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10008#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*isFlag=1#是否置顶，0/1
<<<
success
{
    "msg": "置顶聊天设置成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "置顶聊天设置失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 切换当前聊天对象[K10009]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10009#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
<<<
success
{
    "msg": "切换当前聊天对象成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "切换当前聊天对象失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 获取群成员列表[K10010]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10010#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#群id，勿填错
<<<
success
{
    "msg": "获取群成员列表成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "获取群成员列表失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 获取企业群成员列表[K10011]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10011#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#群id，勿填错
<<<
success
{
    "msg": "获取企业群成员列表成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "获取企业群成员列表失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 创建群聊[K10012]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10012#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#wxid，用英文逗号分隔
<<<
success
{
    "msg": "创建群聊成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "创建群聊失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 修改群聊名称[K10013]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10013#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#群id，勿填错
*newName=新名称#新的群名称
<<<
success
{
    "msg": "修改群聊名称成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "修改群聊名称失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 发布群公告[K10014]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10014#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#群id，勿填错
*newMsg=新公告#公告内容
<<<
success
{
    "msg": "发布群公告成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "发布群公告失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 邀请群成员40人以上[K10015]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10015#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#群id，勿填错
*newWxid#邀请进群的wxid
<<<
success
{
    "msg": "邀请群成员成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "邀请群成员失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 添加群成员40人以下[K10016]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10016#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#群id，勿填错
*newWxid#邀请进群的wxid
<<<
success
{
    "msg": "添加群成员成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "添加群成员失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 删除群成员[K10017]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10017#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#群id，勿填错
*oldWxid#群成员id
<<<
success
{
    "msg": "删除群成员成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "删除群成员失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 退出群聊[K10018]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10018#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#群id，勿填错
<<<
success
{
    "msg": "退出群聊成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "退出群聊失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 获取群内昵称[K10019]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10019#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#群id，勿填错
*oldWxid#群成员id
<<<
success
{
    "msg": "获取群内昵称成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "获取群内昵称失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 修改群内昵称[K10020]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10020#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#群id，勿填错
*newMsg#新的群内昵称
<<<
success
{
    "msg": "修改群内昵称成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "修改群内昵称失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 显示或隐藏群成员昵称[K10021]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10021#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#群id，勿填错
*isFlag=1#是否隐藏，0/1
<<<
success
{
    "msg": "显示或隐藏群成员昵称成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "显示或隐藏群成员昵称失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 保存到通讯录[K10022]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10022#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*isFlag=1#是否保存，0/1
<<<
success
{
    "msg": "保存到通讯录成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "保存到通讯录失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 获取群成员邀请信息[K10023]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10023#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
<<<
success
{
    "msg": "获取群成员邀请信息成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "获取群成员邀请信息失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 获取通讯录列表[K10024]
此处获取的好友+群等(具体自己测试)
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10024#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
<<<
success
{
    "msg": "获取通讯录列表成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "获取通讯录列表失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 获取企业好友列表[K10025]
此处获取的好友+群等(具体自己测试)
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10025#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
<<<
success
{
    "msg": "获取企业好友列表成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "获取企业好友列表失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 获取指定好友信息[K10026]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10026#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
<<<
success
{
    "msg": "获取指定好友信息成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "获取指定好友信息失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 网络获取指定好友信息[K10027]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10027#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
<<<
success
{
    "msg": "网络获取指定好友信息成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "网络获取指定好友信息失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 删除好友[K10028]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10028#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 修改好友备注[K10029]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10029#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*newMsg#新备注
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 同意好友请求[K10030]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10030#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*v3#接收到的消息里获取
*v4#接收到的消息里获取
*sence#接收到的消息里获取
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 好友状态检测[K10031]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10031#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 拉黑好友[K10032]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10032#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*isFlag=1#是否拉黑，0/1
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 发送文本信息[K10033]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10033#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*msg#消息内容
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 发送图片信息[K10034]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10034#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*msg#图片路径，支持网址(直链，如：http://127.0.0.1/tp.jpg)
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 发送文件信息[K10035]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10035#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*msg#文件路径，本地(鲲鹏机器人所在电脑/服务器)
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 发送GIF信息[K10036]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10036#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*msg#GIF路径，支持网址(直链，如：http://127.0.0.1/tp.gif)
<<<
success
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 发送艾特信息[K10037]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10037#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*msg#内容
*list#艾特的wxid列表，用英文逗号隔开，艾特全体填notify@all
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 发送名片信息[K10038]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10038#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*tjWxid#wxid和v4都可以
*tjName#推荐昵称
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 发送链接信息[K10039]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10039#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*title#标题
*desc#描述
*url#链接
*pic#图片路径，支持网址(直链，如：http://127.0.0.1/tp.jpg)
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 发送小程序信息[K10040]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10040#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*xml#自己看收到的xml
*pic#略缩图路径，支持网址(直链，如：http://127.0.0.1/tp.jpg)
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 转发信息[K10041]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10041#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*msgId#消息Id，SvrId
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 取登录状态[K10042]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10042#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 撤回信息[K10043]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10043#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标id，勿填错
*msgId#消息Id，SvrId或者LocalId，自己测测
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
*****
### 获取个人信息[K10044]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10044#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
### 取登录账号列表[K10045]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10045#API代码，必须有
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
### 下载图片[K10046]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10046#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*xml#接收到的消息xml
*path#保存路径，绝对路径，带后缀
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
### 解密图片[K10047]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10047#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*filepath#接收消息里的filepath字段
*path#保存路径，绝对路径，带后缀
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
### 发送XML信息[K10048]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10048#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标ID，勿填错
*xml#XML信息
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
### 刷新朋友圈[K10049]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10049#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
### 获取朋友圈下一页[K10050]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10050#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*circleId#itemid朋友圈ID，获取从该ID的下一条开始的一页
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
### 获取个人朋友圈[K10051]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10051#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*fromWxid#目标ID
*circleId#itemid朋友圈ID，获取从该ID的下一条开始的一页
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
### 朋友圈点赞[K10052]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10052#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*circleId#itemid朋友圈ID，获取从该ID的下一条开始的一页
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
### 朋友圈取消点赞[K10053]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10053#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*circleId#itemid朋友圈ID，获取从该ID的下一条开始的一页
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
### 发表朋友圈评论[K10054]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10054#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*circleId#itemid朋友圈ID，获取从该ID的下一条开始的一页
*msg#评论的内容
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
### 删除朋友圈评论[K10055]
~~~[api]
post:http://127.0.0.1:2022/KP
*api=K10055#API代码，必须有
*robotWxid=wxid_xxxxxxxxxx#机器人的wxid
*circleId#itemid朋友圈ID，获取从该ID的下一条开始的一页
<<<
success
{
    "msg": "成功",
    "code": 200,
    "success": true,
    "data": {}
}
<<<
error
{
    "msg": "失败",
    "code": 101,
    "success": true,
    "data": {}
}
~~~
