# 说明 #
* HEAD附带参数
  * version-code：版本号
  * version-name：版本名称
  * device-id：设备唯一id号
  * channel-id：渠道编号「umemg、wandoujia」
  * platform：平台类型「ios、android」

* code说明
  * 0代表成功，非0代表失败

* message 「code说明」

# API 

## 用户模块 (地址：http://liu.duanz.in/api/v1/account/login)
* 登录 (http://liu.duanz.in/api/v1/account/login)
  * 地址: POST /api/v1/account/login
  * 参数：
    * phone：手机号码
    * password：密码
  * 返回结果
    * code
    * message
    * data
      * account obj

* 注册 (http://liu.duanz.in/api/v1/account/register)
  * 地址：POST /api/v1/account/register
  * 参数：
    * phone：手机号
    * captcha：验证码
    * password：密码
    * role：角色「0-托运方、1-承运方」
  * 返回结果：
    * code
    * message
    * data
      * account obj

* 忘记密码 (http://liu.duanz.in/api/v1/account/forgetPassword)
  * 地址：POST /api/v1/account/forgetPassword
  * 参数：
    * phone：手机号
    * captcha：验证码
    * password：密码
  * 返回结果：
    * code
    * message
    * data
      * account obj

* 修改密码 (http://liu.duanz.in/api/v1/account/updatePassword)
  * 地址：POST /api/v1/account/updatePassword
  * 参数：
    * account_id：登录用户id
    * token：登录凭证
    * old_password：旧密码
    * password：新密码
  * 返回结果：
    * code
    * message
    * data
      * account obj

* 获取验证码：（(http://liu.duanz.in/api/v1/account/captcha)暂固定返回验证码字符串为123456，服务器保存30分钟）
  * 地址：GET /api/v1/account/captcha
  * 参数：
    * phone：手机号
  * 返回结果
    * code
    * message
    * data
      * str

* 修改用户资料：(http://liu.duanz.in/api/v1/account/update)
  * 地址：POST /api/v1/account/update
  * 参数：
  	* account_id：登录用户id
    * token：登录凭证
    * name：姓名 [可选]
    * avatar：图像 [可选]
  * 返回结果
    * code
    * message
    * data
      * account obj

* 用户详情：(http://liu.duanz.in/api/v1/account/detail)
  * 地址：GET /api/v1/account/detail
  * 参数：
    * account_id：用户id
  * 返回结果
    * code
    * message
    * data
      * account obj
          * driver obj

## 钱包相关
* 提现：(http://liu.duanz.in/api/v1/wallet/withdraw)
  * 地址: POST /api/v1/wallet/withdraw
  * 参数：
    * account_id：用户id
    * token：用户登录凭证
    * amount：提现金额
  * 返回结果
    * code
    * message

* 钱包支付：(http://liu.duanz.in/api/v1/wallet/pay)
  * 地址: POST /api/v1/wallet/pay
  * 参数：
    * account_id：用户id
    * token：用户登录凭证
    * amount：提现金额
  * 返回结果
    * code
    * message    

* 收支明细：(http://liu.duanz.in/api/v1/wallet/log)
  * 地址: GET /api/v1/wallet/log
  * 参数：
    * account_id：用户id
    * token：用户登录凭证
    * page：页码
    * page_size：单页大小
  * 返回结果
    * code
    * message
    * page_size：
    * total_size：
    * data
      * simple wallet_log obj

* 收支明细详情：(http://liu.duanz.in/api/v1/wallet/detail)
  * 地址: GET /api/v1/wallet/detail
  * 参数：
    * account_id：用户id
    * token：用户登录凭证
    * wallet_log_id：明细id
  * 返回结果
    * code
    * message
    * data
      * wallet_log obj

## 评论API

* 顾客评论列表：(http://liu.duanz.in/api/v1/comment/list)
  * 地址：GET /api/v1/comment/list
  * 参数：
    * driver_id：用户id
    * page：页码
    * page_size：单页大小
  * 返回结果：
    * code
    * message
    * page：当前页
    * page_size：单页条数
    * total_size：总条数
    * data
      * comment obj
        * simple account obj

* 评论：(http://liu.duanz.in/api/v1/comment/post)
  * 地址：POST /api/v1/comment/post
  * 参数：
    * consignor_id：托运人id
    * token：用户登录凭证
    * driver_id：承运人id
    * content：内容
    * rating：星级
  * 返回结果
    * code
    * message
    * data
      * goods obj

## 货源相关
* 发布货源：(http://liu.duanz.in/api/v1/goods/publish)
  * 地址：POST /api/v1/goods/publish
  * 参数：
    * consignor_id：托运人id
    * token：用户登录凭证
    * start_address：起运地
	  * end_address：目的地
	  * category：种类
	  * weight：重量「单位-吨」
	  * number：货物件数
	  * start_time：起运时间
	  * end_time：到达时间
    * loading_address：装货地址
    * unload_address：卸货地址
    * worth：货物价值 [ optional]
    * squares：货物立方数「单位-立方米」[ optional]
    * picture：货物图片 [ optional]
    * remark：备注 [ optional]
  * 返回结果
    * code
    * message
    * data
      * good obj

* 取消货源：(http://liu.duanz.in/api/v1/goods/cancel)
  * 地址：POST /api/v1/goods/cancel
  * 参数：
    * token：用户登录凭证
    * good_id：货源id
  * 返回结果
    * code
    * message
    * data
      * good obj

* 货源列表：(http://liu.duanz.in/api/v1/goods/list)
  * 地址：GET /api/v1/goods/list
  * 参数：
    * driver_id：承运人id
    * token：用户登录凭证
  * 返回结果
    * code
    * message
    * data
      * good obj
        * account obj
        * freight obj

## 报价相关API
* 承运人提交报价：(http://liu.duanz.in/api/v1/freight/submit)
  * 地址：POST /api/v1/freight/submit
  * 参数：
    * account_id：承运人id
    * token：用户登录凭证
    * good_id：货源id
    * unit：单位「0-吨位、1-立方」
    * price：价格「单位元」
  * 返回结果
    * code
    * message
    * data
      * freights obj

* 报价列表：(http://liu.duanz.in/api/v1/freight/list)
  * 地址：GET /api/v1/freight/list
  * 参数：
    * token：用户登录凭证
    * good_id：货源id
  * 返回结果
    * code
    * message
    * data
      * freights obj
        * simple account obj

* 承运人的最新报价：(http://liu.duanz.in/api/v1/freight/lastest)
  * 地址：GET /api/v1/freight/lastest
  * 参数：
    * freight_id：货源id
  * 返回结果
    * code
    * message
    * data
      * freights obj

* 承运人修改报价：(http://liu.duanz.in/api/v1/freight/update)
  * 地址：POST /api/v1/freight/update
  * 参数：
    * token：用户登录凭证
    * freight_id：报价id
    * unit：单位
    * price：价格
  * 返回结果
    * code
    * message
    * data
      * freights obj

* 忽略报价：（http://liu.duanz.in/api/v1/freight/ignore）
  * 地址：POST /api/v1/freight/ignore
  * 参数：
    * token：凭证
    * good_id：货源id
    * account_id：承运人id
  * 返回结果
    * code
    * message
    * data

## 订单相关API
* 提交订单：(http://liu.duanz.in/api/v1/order/submit)
  * 地址：POST /api/v1/order/submit
  * 参数：
    * consignor_id：托运人id
    * token：用户登录凭证
	  * driver_id：承运人id
    * goods_id：货源id
    * amount：金额
  * 返回结果
    * code
    * message
    * data
      * order obj

* 订单状态更新：(http://liu.duanz.in/api/v1/order/update)
  * 地址：POST /api/v1/order/update
  * 参数：
    * token：用户登录凭证
    * order_id：订单id
    * status：状态「0-待支付、1-待出发、2-等待撤单、3-已撤单、4-已出发(装货完成)、5-卸货完成、6确认到达」
  * 返回结果
    * code
    * message
    * data
      * order obj

* 订单详情：(http://liu.duanz.in/api/v1/order/detail)
  * 地址：GET /api/v1/order/detail
  * 参数：
    * account_id：登录用户id
    * token：用户登录凭证
    * order_id：订单id
  * 返回结果
    * code
    * message
    * data
      * good obj
      * account obj
      * amount str

* 订单列表：(http://liu.duanz.in/api/v1/order/list)
  * 地址：GET /api/v1/order/list
  * 参数：
    * account_id：登录用户id
    * token：登录凭证
    * role：角色「0-托运方、1-承运方」
    * status：状态「0-未支付|待支付、1-待出发、2-已出发、3-已完成|已达到」
    * page：页码
    * page_size：单页大小
  * 返回结果：
    * code
    * message
    * page：当前页
    * page_size：单页条数
    * total_size：总条数
    * data
      * order obj
        * consignor obj
        * good obj
        * driver obj
      

## 系统模块
* 初始化：（http://liu.duanz.in/api/v1/system/initialize）
  * 地址：GET /api/v1/system/initialize
  * 参数：无
  * 返回结果：
    * code
    * message
    * data
      * configs arary

* 注册推送通知：（http://liu.duanz.in/api/v1/system/registerPushId）
  * 地址：POST /api/v1/system/registerPushId
  * 参数：
    * app_user_id：推送用户
    * app_channel_id：推送渠道
    * account_id：用户id
  * 返回结果：
    * code
    * message
    * data
      * push obj

* 版本更新：(http://liu.duanz.in/api/v1/system/checkVersion)
  * 地址: GET /api/v1/system/checkVersion
  * 参数：无
  * 返回结果
    * code
    * message
    * data
      * version obj

* 意见反馈：(http://liu.duanz.in/api/v1/system/feedback)
  * 地址: POST /api/v1/system/feedback
  * 参数：
    * account_id：用户id
    * content：反馈内容
    * contact：联系方式（optional）
  * 返回结果
    * code
    * message

## 承运人模块
* 承运人提交 [http://liu.duanz.in/api/v1/account/driverWrite]
  * 参数：
    * account_id
    * name
    * idcard
    * address
    * no_bank
    * no
    * open_name
    * open_bank
    * type
    * primary_no
    * primary_owner
    * primary_phone
    * primary_address
    * frame_no
    * engine_no
    * primary_register_time
    * tonnage
    * len
    * volume [ optional]
    * use [ optional]
    * is_secondary
    * secondary_no [ optional]
    * secondary_owner [ optional]
    * secondary_phone [ optional]
    * secondary_address [ optional]
    * secondary_register_time [ optional]
    * is_insurance [ optional]
    * remark [ optional]
    * driver_icon
    * drivers_license array
    * driving_license array
    * service_license array
    * car_photo array
    * register_license [ optional]
    * policy [ optional]
    * transport_good array [ optional]
    * transport_line array [ optional]
  * 返回结果
    * code
    * message

* (废弃)支付保证金 [POST http://liu.duanz.in/api/v1/account/deposit]
  * 参数：
    * account_id：用户id
    * amount：金额
    * token：
  * 返回结果
    * code
    * message
    * data
      * account obj    

## 支付接口
  * 订单支付 [POST http://liu.duanz.in/api/v1/pay/charge]
    * 参数：
      * account_id：用户id
      * order_id：订单id [optional]
      * business_type：业务类型 [0-支付运费、1-支付保证金]
      * amount：订单金额
      * channel：支付渠道 [alipay]
    * 返回结果
      * data
        * pay obj  















