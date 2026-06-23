---
title: Personal模块下线API清单
domain: payby-open-api
kind: wiki_page
slug: personal-api-offline-list
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:b3f96fd2-366d-4cdc-9016-50a6e3111061
tags: []
---

# Personal模块下线API清单

本页汇总 `payby-open-api` 业务域中 Personal 模块拟下线 API 的访问统计、Gateway 类型、负责人及下线确认状态（基于最近一个月访问数据）。

## 字段说明

- **API Code**：接口路径
- **API Name**：接口中文名
- **Gateway Type**：网关类型，取值 `CGS` / `SGS`
- **Last Access Time**：最近一次访问时间，`~` 表示无访问记录
- **Access Rate(In Last 1 Month)**：最近一个月访问次数，`~` 表示 0
- **Owner**：负责人
- **Offline Confirmation**：下线确认，`Y` 表示已确认下线

## 已确认下线（Offline Confirmation = Y）

无近一个月访问记录，且 owner 已确认下线：

| API Code | API Name | Gateway | Owner |
|---|---|---|---|
| /personal/sms/sendbyphone | 根据手机号发送短信 | CGS | Yadong Lu |
| /personal/paypassword/reset | 忘记支付密码初始化 | CGS | Yadong Lu |
| /personal/paypassword/modify | 修改支付密码 | CGS | Yadong Lu |
| /personal/paypassword/verify | 验证支付密码 | CGS | Yadong Lu |
| /personal/bill/detailByOutOrderNo | 查询订单详情通过商户订单号-已授权 | CGS | - |
| /personal/auth/login | 授权登陆 | CGS | Zhibin Liu |
| /personal/transfer/query | 提现查询 | CGS | Zhibin Liu |
| /personal/bill/tradeDetail | 账单详情-已授权 | CGS | Zhibin Liu |
| /personal/pushDeviceInfo | 保存设备信息接口 | CGS | Zhibin Liu |
| /personal/merchant/checkDetails | 个人商户查看收款明细 | CGS | Zhibin Liu |
| /personal/merchant/homepage | 个人商户查看主页 | CGS | Zhibin Liu |
| /personal/log/pushAppLog | APP上传错误信息 | CGS | Zhibin Liu |
| /personal/v2/paypassword/modify/init | 修改支付密码初始化接口 | CGS | Meimei Huang |
| /personal/v2/paypassword/modify/verifyIdn | 修改支付密码校验kyc接口 | CGS | Meimei Huang |
| /personal/v2/paypassword/modify/verifyPwd | 修改支付密码校验密码接口 | CGS | Meimei Huang |
| /personal/v2/paypassword/modify | 修改支付密码接口 | CGS | Meimei Huang |
| /personal/card/payment/bind/init | 绑卡初始化接口 | CGS | - |
| /personal/common/v1/change-mobile/confirm | change mobile | SGS | Meimei Huang |
| /personal/common/v1/change-mobile/verify | ticket verify | SGS | Meimei Huang |

## 待确认下线（无访问、无 Y 标记）

最近一个月访问量为 `~`（即 0），但 Offline Confirmation 列尚未标记 `Y`，按 Owner 分组：

### Sai Yu

- /personal/withdraw/submit 提现提交（CGS）
- /personal/withdraw/list 提现历史记录查询（CGS）
- /personal/common/exchange 金额转换（CGS）
- /personal/card/PasswordVerify 解绑卡密码校验（CGS）
- /personal/pushVip VIP推送（SGS）
- /personal/sendActivityEvent 发送活动事件（SGS）
- /personal/auth/loginByAuthCode 授权码登录（CGS）
- /personal/auth/oauthByAuthCode 授权码授权（CGS）
- /personal/auth/followOA 关注公众号（CGS）
- /personal/sendPaySms 发送短信支付验证码（CGS）
- /personal/smsPay 短信支付（CGS）
- /personal/appeal/queryAppealHistory 查询诉求历史（CGS）
- /personal/otpLoginVerifySms otp-login验证短信验证码（CGS）
- /personal/appeal/appendAppealDataUn 追加资料-非授权（CGS）
- /personal/bank/setNickname 设置昵称（CGS）
- /personal/transfer/bank/list 转账到银行账户历史记录（CGS）
- /personal/cbr/v1/auth/init 跨境汇款初始化（CGS）
- /personal/cbr/v1/auth/query-bank-info 查询卡信息（CGS）
- /personal/cbr/v1/auth/add-beneficiary 添加收益人（CGS）
- /personal/cbr/v1/auth/query-beneficiary-list 查询收益人列表（CGS）
- /personal/cbr/v1/auth/submit 汇款提交（CGS）
- /personal/cbr/v1/auth/remittance-try-calculate 汇款试算（CGS）
- /personal/appeal/v1/auth/query-un-trade-appeal-info 查询未授权交易申诉详情（CGS）
- /personal/card/v1/auth/save-ocr-info 保存支付卡ocr信息（CGS）
- /personal/queryTransactions 查询交易记录（SGS）

### Zhibin Liu

- /personal/transfer/receipt 转账-领取收款（CGS）
- /personal/member/preference/query 查询偏好设置（CGS）
- /personal/risk/pushWhite 风控白名单推送（SGS）
- /personal/transfer/scanTransfer 扫码转账-扫收款码（CGS）
- /personal/common/unBindCard 解绑卡（CGS）
- /personal/common/user/message/list 查询用户消息列表（CGS）
- /personal/message/unbindPushToken 解绑pushToken（CGS）
- /personal/batchUnbindCard 批量解绑卡（CGS）
- /personal/withdraw/tryCalculateFee 提现试算费（CGS）
- /personal/v2/withdraw/submit 提现V2接口（CGS）
- /personal/card/parseCardNo 解析卡号接口（CGS）
- /personal/card/bindCard 绑卡（CGS）
- /personal/queryFilterCondition 查询过滤条件（SGS）

### Yadong Lu

- /personal/kyc/verifyEid ICA认证（CGS）
- /personal/kyc/verifyLiveFace 活体认证（CGS）
- /personal/kyc/verifyIdn 实名信息校验（CGS）
- /personal/kyc/verifyIdn/direct 直接校验实名（CGS）
- /personal/v2/sms/sendbyphone 根据手机号发短信（CGS）
- /personal/v2/sms/verify 未授权的短信验证接口（CGS）
- /personal/v2/paypassword/reset 找回支付密码（CGS）
- /personal/v2/paypassword/forget/init 忘记支付密码初始化（CGS）
- /personal/v2/kyc/verifyIdn 身份证验证（CGS）
- /personal/sms/areaCode 获取区号（CGS）
- /person
