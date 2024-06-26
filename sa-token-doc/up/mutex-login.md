# 同端互斥登录

如果你经常使用腾讯QQ，就会发现它的登录有如下特点：它可以手机电脑同时在线，但是不能在两个手机上同时登录一个账号。 <br/>
同端互斥登录，指的就是：像腾讯QQ一样，在同一类型设备上只允许单地点登录，在不同类型设备上允许同时在线。


<button class="show-img" img-src="https://oss.dev33.cn/sa-token/doc/g/g3--mutex-login.gif">加载动态演示图</button>

--- 

## 具体API

在 Sa-Token 中如何做到同端互斥登录? <br/>
首先在配置文件中，将 `isConcurrent` 配置为false，然后调用登录等相关接口时声明设备类型即可：


#### 指定设备类型登录
``` java
// 指定`账号id`和`设备类型`进行登录
StpUtil.login(10001, "PC");	
```
调用此方法登录后，同设备的会被顶下线（不同设备不受影响），再次访问系统时会抛出 `NotLoginException` 异常，场景值=`-4`


#### 指定设备类型强制注销
``` java
// 指定`账号id`和`设备类型`进行强制注销 
StpUtil.logout(10001, "PC");	
```
如果第二个参数填写null或不填，代表将这个账号id所有在线端强制注销，被踢出者再次访问系统时会抛出 `NotLoginException` 异常，场景值=`-2`


#### 查询当前登录的设备类型
``` java
// 返回当前token的登录设备类型
StpUtil.getLoginDevice();	
```


#### Id 反查 Token
``` java
// 获取指定loginId指定设备类型端的tokenValue 
StpUtil.getTokenValueByLoginId(10001, "APP");	
```


--- 

<a class="case-btn" href="https://gitee.com/dromara/sa-token/blob/master/sa-token-demo/sa-token-demo-case/src/main/java/com/pj/cases/up/MutexLoginController.java"
	target="_blank">
	本章代码示例：Sa-Token 同端互斥登录  —— [ MutexLoginController.java ]
</a>