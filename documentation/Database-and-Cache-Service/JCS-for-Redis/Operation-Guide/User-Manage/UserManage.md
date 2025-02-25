# 账号管理

通过账号管理功能，云缓存Redis实例支持创建多个账号，并对账号配置读写或只读权限，以满足复杂业务场景中对业务权限的控制，从而最大限度地避免误操作和提升数据安全性。

## 注意事项


密码访问模式下该功能才生效。

-  在密码访问模式状态下，支持对实例分配读写或只读权限，且所配置的用户鉴权一分钟内生效。

-  免密模式下，访问Redis实例无需鉴权。

-  修改读写或只读权限，将会对新建连接生效，而存量连接将保留原有策略不变。

目前云缓存Redis提供支持 的版本为Redis4.0，Redis2.8不再支持。

该功能对新建的实例默认开放，对于该功能上线前的存量实例需要进行升级才能使用。如果您需要在原有实例使用该功能，可联系我们并告知实例ID和升级时间，待升级完成后即可使用。

针对每个实例，每个用户Pin能创建20个账号，如需更多可提交工单申请。



## 账号分类

#### 默认账号：

访问实例的默认账号，只有密码没有账号名，默认拥有读写权限，可修改密码，但不能删除。

创建实例时，如果关闭免密并配置了密码，则该密码即为默认账号的密码。

``` 
// 连接示例：
redis-cli -a password
```


#### 自定义账号

由用户自定义的账号，可分配只读权限和读写权限，在密码访问模式下需要通过用户名和密码才能访问实例，该类账号的数量上限为20个。

``` 
// 连接示例：
redis-cli -h ip -p port -a username:password
```



## 权限分类

只读权限：账号只有读取数据的权限，无修改数据的权限。

读写权限：账号具有读和写数据的权限。

## 操作步骤

### 查看和使用账号管理功能

1.登录[Redis 控制台](https://redis-console.jdcloud.com/redis)。

2.在"实例列表"页面，选择目标实例，点击 实例名称，进入"实例详情"页面。在"实例详情"页面，点击 参数配置 tab签页面，进入"命令禁用管理"页面。

3.在"账号管理"页面，可以看到已经配置的账号列表，并执行创建账号、修改权限、修改密码、删除账号、修改备注操作。

![](../../../../../image/Redis/UserManage-1.png)

4.使用账号管理功能，需在密码访问模式下才能使用。因此，您需要先关闭“免密访问”。

在免密模式下：

-  访问Redis实例无需鉴权。

-  账号管理中的创建账号、修改权限、修改密码、删除账号、修改备注操作，均无法使用。

在密码访问模式下：

-  在密码访问模式状态下，支持对实例分配读写或只读权限，且所配置的用户鉴权一分钟内生效。

-  在关闭“免密访问”后，如果列表中已经存在账号，则该账号权限直接生效。

-  在关闭“免密访问”时设置的密码，为默认账号的密码。

![](../../../../../image/Redis/UserManage-2.png)


### 创建账号

使用创建账号功能时：

-  在密码访问模式状态下才能创建账号。

-  创建的账号的类型，均为“自定义账号”，该类账号用户可以进行增删改查。

-  创建完账号后如果列表中并未出现，可点击刷新按钮。

![](../../../../../image/Redis/UserManage-3-1.png)


### 修改权限

使用修改权限功能时，修改将会对新建连接生效，而存量连接将保留原有策略不变。

![](../../../../../image/Redis/UserManage-4-1.png)


### 删除账号

账号删除后，将不能访问当前实例。

![](../../../../../image/Redis/UserManage-5-1.png)


### 修改密码

对于用户自定义账号的密码，可在账号管理中直接进行操作修改。

![](../../../../../image/Redis/UserManage-6-1.png)

对于默认账号的密码，可在3个入口进行修改：

-  在当前“账号管理”页中，对默认账号进行密码修改。

-  实例详情页中，“资源信息”tab页中的访问信息部分，关闭免密访问后所配置的密码，以及“连接密码”处修改密码时所配置的密码。

-  实例详情页中，右上角“操作”中的“修改密码”操作。




## 常见问题

**Q：当把实例从密码访问改为免密访问模式后，使用原用户名密码访问为何会报错？**

A：可在“参数配置”中，修改@no-auth-ignore 参数值为 yes。当重新改回为密码访问后，再将该参数值恢复为默认值no。







