### 1. 功能说明

#### 1.1 支持币种

USDT(omni  btc)  
USDT(ERC20 eth)  泰达币
USDT(TRC20 trx)

#### 1.2 功能描述
 上述币种的自动归总， 记账功能 以及审核提币功能
#### 1.接口校验
1. 将参数按字典序排序，进行Get请求方式参数拼接
2. 将拼接好的参数列表加入key(向钱包方申请)
3. 将上述拼接好的参数进行md5摘要运算
4. 将上述运算出来的值加入参数列表，参数名为 **sign**
#### 接口校验事例
例如 传三个参数 a=5 c=6 b=10
首先按字典序拼接三个参数
```
a=5&b=10&c=6
```
拼接好的字符串加入key(key放最后不需要排序)
```
a=5&b=10&c=6&key=1
```

然后进行md5
```
md5("a=5&b=10&c=6&key=1")
```
那么总体参数就是
```
{
   "a":"5",
   "b":"10",
   "c":"6",
   "sign":"cc1877fcffebcfd9528c657d0abeb412",
}
```


#### 1.3 接口请求方法 
所有接口目前采用``` POST ```方式  
参数传递采用  ```  application/json  ```




##### 1.4 公共参数（所有接口均需配这三个公共参数）

参数名 | 是否必须| 参数说明
---|---| ---
appId | Y | appId（向管理端申请）
sign | Y | 参数签名
time | Y | 时间戳(秒)
 
 
 ### 2. 接口
#### 2.1 创建地址接口
```
/${addressType}/create
```

``` ${addressType} ```为地址类型 目前支持 BTC(OMNI) 或者ETH（ERC20）或者 TRX(TRC20)
参数名 | 是否必须| 参数说明
---|---| ---
userId | Y | 用户Id


#### 2.2 审核发币接口
```
/send
```

``` ${addressType} ```为地址类型 目前支持 BTC 或者ETH 或者TRX
参数名 | 是否必须| 参数说明
---|---| ---
address | Y | 用户地址
addressType | Y | 地址类型(BTC 或者ETH) 或者TRX
series | Y | 系列(比特币传BTC 以太坊传ETH USDT 传 OMNI 或者 ERC20) 或者TRC20
amount | Y | 数量
coin | Y | 币种（见1中支持的币种）



#### 2.3 通知接口(钱包方主动调用接口告诉平台用户充值)

参数名 | 是否必须| 参数说明
---|---| ---
addr | Y | 用户地址
addressType | Y | 地址类型(BTC 或者ETH 或者TRX)
time | Y | 时间
hash | Y | 交易hash  正常来说不会重复通知， 但是平台方需要保存好这个hash 如果这个hash已经存入 则此条通知应作废
coin | Y | 币种
amount | Y | 数量
userId | Y | 用户ID
sign | Y | 签名


#### 地址页面
使用
```
https://www.a3ipay.com/#/address?address=${address}&coinType=${coinType}
```
使用通过创建地址创建的地址 和币种 替换上述中的${address} 和 ${coinTyp}






