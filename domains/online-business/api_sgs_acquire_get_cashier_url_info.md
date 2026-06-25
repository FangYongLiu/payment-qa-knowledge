---
id: api_sgs_acquire_get_cashier_url_info
object_type: API
name: 查询收银台URL信息接口(acquire2/getCashierUrlInfo)
aliases: [getCashierUrlInfo]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: 接口文档
source_ref: PayBy API v2.25 p15
tags: [online-business, acquiring, SGS, 收银台, 二维码]
related_services: [svc_sgs, svc_acquireii]
related_tables: []
related_scenarios: [scn_online_business_cashier_pay]
---

# 查询收银台URL信息接口(acquire2/getCashierUrlInfo)

## 用途
查询收银台二维码(tokenUrl)是否已被用户扫描,以及扫描者的脱敏信息(用于收银台「等待付款」状态展示)。

## 关联关系
- **所属服务**:[[svc_sgs]] → [[svc_acquireii]](= `related_services`)。
- **被哪些场景测**:[[scn_online_business_cashier_pay]]。
- **tokenUrl 来源**:下单 [[api_sgs_acquire_place_order]] 返回的 interactionParams.tokenUrl。

## 路径 / 方法
- 联调:`https://uat.test2pay.com/sgs/api/acquire2/getCashierUrlInfo`;生产:`https://api.payby.com/sgs/api/acquire2/getCashierUrlInfo`;POST(JSON)。

## 入参
bizContent = GetCashierUrlInfoRequest:`tokenUrl`(收银台 URL,如 `https://checkout.payby.com/pay-page/main?BIZ_TYPE=202&ft=xxx&t=xxx`)。

## 出参
bizBody = GetCashierUrlInfoResponse:`payer`(Payer:`mobileNumberMask` 脱敏手机号,如 `+971-58*****92`)。

## 错误码
通用码见 [[reference_acquire_protocol_and_codes]]。特有:`62082 TOKEN_URL_NOT_EXIST`(tokenUrl 错误或已失效)。

## 测试校验点(QA)
- tokenUrl 缺失 → INVALID_PARAMETER;错误/失效 → 62082。
- 二维码已扫:payer.mobileNumberMask 返回脱敏格式,**不得泄露完整手机号**。
- 未扫场景下 body/payer 取值规则;仅成功返回 body;`sign` 验签。
