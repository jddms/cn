# modifyForwardRule


## 描述
更新非网站类规则

## 请求方式
PATCH

## 请求地址
https://ipanti.jdcloud-api.com/v1/regions/{regionId}/instances/{instanceId}/forwardRules/{forwardRuleId}

|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**regionId**|String|True| |区域 ID, 高防不区分区域, 传 cn-north-1 即可|
|**instanceId**|String|True| |高防实例 Id|
|**forwardRuleId**|String|True| |转发规则 Id|

## 请求参数
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**forwardRuleSpec**|[ForwardRuleSpec](modifyforwardrule#forwardrulespec)|True| |更新非网站类规则请求参数|

### <div id="forwardrulespec">ForwardRuleSpec</div>
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**protocol**|String|True| |协议: TCP 或者 UDP|
|**serviceIp**|String|False| |高防 IP, serviceIps 为空时生效|
|**serviceIps**|String[]|False| |高防 IP 列表, 不为空时忽略 serviceIp, 传多个时后台会在高防IP封禁后随机切换其他未封禁的IP|
|**port**|Integer|True| |端口号, 取值范围[1, 65535]|
|**algorithm**|String|True| |转发规则. <br>- wrr: 带权重的轮询<br>- rr:  不带权重的轮询<br>- sh:  源地址hash|
|**originType**|String|True| |回源类型: A 或者 CNAME|
|**originAddr**|[OriginAddrItem[]](modifyforwardrule#originaddritem)|False| | |
|**onlineAddr**|String[]|False| |备用的回源地址列表, 可以配置为一个域名或者多个 ip 地址|
|**originDomain**|String|False| |回源域名|
|**originPort**|Integer|True| |回源端口号, 取值范围[1, 65535]|
### <div id="originaddritem">OriginAddrItem</div>
|名称|类型|是否必需|默认值|描述|
|---|---|---|---|---|
|**ip**|String|False| |回源ip|
|**weight**|Integer|False| |权重|
|**inJdCloud**|Boolean|False| |是否为京东云内公网ip|

## 返回参数
|名称|类型|描述|
|---|---|---|
|**result**|[Result](modifyforwardrule#result)| |
|**requestId**|String| |
|**error**|[Error](modifyforwardrule#error)| |

### <div id="error">Error</div>
|名称|类型|描述|
|---|---|---|
|**err**|[Err](modifyforwardrule#err)| |
### <div id="err">Err</div>
|名称|类型|描述|
|---|---|---|
|**code**|Long|同http code|
|**details**|Object| |
|**message**|String| |
|**status**|String|具体错误|
### <div id="result">Result</div>
|名称|类型|描述|
|---|---|---|
|**code**|Integer|0: 更新规则失败, 1: 更新规则成功|
|**message**|String|更新规则失败时给出具体原因|

## 返回码
|返回码|描述|
|---|---|
|**200**|OK|
