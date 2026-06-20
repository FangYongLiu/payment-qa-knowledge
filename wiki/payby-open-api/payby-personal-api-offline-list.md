---
title: PayBy Personal API 下线清单与访问统计
domain: payby-open-api
kind: wiki_page
slug: payby-personal-api-offline-list
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
source_type: wiki
source_ref: confluence:PMDPayment/969048485
tags: []
---

# PayBy Personal API 下线清单与访问统计

本页汇总待下线的 `/personal` 系列 API 清单，涵盖 API Code、名称、Gateway Type、最近一个月访问情况、Owner 与下线确认状态（Offline Confirmation）。统计窗口为最近一个月，"~" 表示无访问记录。

## 字段说明

- **API Code**：接口路径，原样保留。
- **API Name**：接口中文名。
- **Gateway Type**：网关类型，取值 `CGS` 或 `SGS`。
- **Last Access Time**：最近一次访问时间。
- **Access Rate (In Last 1 Month)**：最近一个月访问次数。
- **Owner**：负责人。
- **Offline Confirmation**：是否已确认下线，标记 `Y` 表示已确认。

## 无访问记录的接口（Last Access Time = ~）

### 已确认下线（Offline Confirmation = Y）

| API Code | API Name | Gateway | Owner |
|---|---|---|---|
| /personal/sms/sendbyphone | 根据手机号发送短信 | CGS | Yadong Lu |
| /personal/paypassword/reset | 忘记支付密码初始化 | CGS | Yadong Lu |
| /personal/paypassword/modify | 修改支付密码 | CGS | Yadong Lu |
| /personal/paypassword/verify | 验证支付密码 | CGS | Yadong Lu |
| /personal/bill/detailByOutOrderNo | 查询订单详情通过商户订单号-已授权 | CGS | （未指定） |
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
| /personal/card/payment/bind/init | 绑卡初始化接口 | CGS | （未指定） |
| /personal/common/v1/change-mobile/confirm | change mobile | SGS | Meimei Huang |
| /personal/common/v1/change-mobile/verify | ticket verify | SGS | Meimei Huang |

### 未确认下线（Offline Confirmation 空）

KYC 与认证类：
- /personal/kyc/verifyEid（ICA认证, Yadong Lu）
- /personal/kyc/verifyLiveFace（活体认证, Yadong Lu）
- /personal/kyc/verifyIdn（实名信息校验, Yadong Lu）
- /personal/kyc/verifyIdn/direct（直接校验实名, Yadong Lu）
- /personal/v2/kyc/verifyIdn（身份证验证, Yadong Lu）
- /personal/kyc/quota（查询NON_KYC额度查询, Yadong Lu）
- /personal/kyc/contract（KYC流程协议签约, Yadong Lu）
- /personal/kyc/sms/verify（KYC流程短信验证, Yadong Lu）
- /personal/kyc/verifyInfo（kyc流程审核信息, Yadong Lu）
- /personal/kyc/auditInfo（kyc流程审核信息, Yadong Lu）
- /personal/kyc/fillup/submitEid（补充提交eid照片, Gangling Shen）
- /personal/kyc/expire/submit（eid过期重新ocr失败手工submit审核, Gangling Shen）
- /personal/kyc/passport/signProtocol（护照认证签订协议, Gangling Shen）
- /personal/kyc/passport/submitPassport（提交护照ocr识别, Gangling Shen）
- /personal/kyc/passport/confirmInfo（护照信息确认, Gangling Shen）
- /personal/kyc/passport/invitationCode（提交邀请码, Gangling Shen）
- /personal/kyc/invitationCode（eid流程保存邀请码接口, Gangling Shen）
- /personal/kyc/passport/info（获取用户护照信息, Yadong Lu）
- /personal/kyc/passport/address（提交地址信息, Yadong Lu）
- /personal/kyc/fillup/v2/recognizeEid（补充eid自动识别, Gangling Shen）
- /personal/kyc/v2/invitation-code（单独提交邀请码, Yadong Lu）
- /personal/kyc/v1/auth/kyc-flag（kyc标记查询, Yadong Lu）
- /personal/kyc/v1/auth/card/query-payment-card-list（kyc已绑卡列表查询, Yadong Lu）
- /personal/kyc/v1/auth/kyc-authorize/apply（kyc授权同步申请, Yadong Lu）
- /personal/kyc/v1/auth/kyc-authorize/confirm（kyc授权同步确认, Yadong Lu）
- /personal/kyc/v1/auth/query-invitation-record（查询推荐人推荐记录信息接口, Gangling Shen）
- /personal/kyc/v1/auth/referral-retry（被推荐人重试kyc接口, Gangling Shen）
- /personal/kyc/v1/auth/start-referrer-kyc（开始推荐人kyc接口, Gangling Shen）
- /personal/kyc/v2/auth/supply-eid/init（推荐人kyc初始化补充eid接口, Gangling Shen）
- /personal/kyc/v3/auth/supply-eid/submit-audit（推荐人kyc提交补充eid接口, Gangling Shen）
- /personal/kyc/v3/auth/supply-eid/upload（推荐人kyc上传eid接口, Gangling Shen）
- /personal/kyc/v2/auth/query-referrerkyc-result（推荐人kyc查询结果接口, Gangling Shen）
- /personal/kyc/v1/auth/eid-info（查询eid明文信息接口, Gangling Shen）
- /personal/kyc/v6/auth/supply-eid/upload（推荐人kyc上传eid的V6接口, Gangling Shen）
- /personal/activate-account/v1/auth/replenish-eid（补充提交ocr识别的eid信息接口, Gangling Shen）
- /personal/activate-account/v1/auth/save-passport（保存前端ocr
