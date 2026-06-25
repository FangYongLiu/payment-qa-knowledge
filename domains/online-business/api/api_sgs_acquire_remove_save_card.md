---
id: api_sgs_acquire_remove_save_card
object_type: API
name: 解绑已保存卡接口(acquire2/removeSaveCard)
aliases: [removeSaveCard]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: 接口文档
source_ref: PayBy API v2.25 p15
tags: [online-business, acquiring, SGS, savedCard, cardToken, 解绑]
related_services: [svc_sgs, svc_acquireii]
related_tables: [tbl_acquireii_t_card_info]
related_scenarios: [scn_online_business_direct_pay]
---

# 解绑已保存卡接口(acquire2/removeSaveCard)

## 用途
将已保存的 `cardToken` 置为失效,使其无法再被查询和使用。

## 关联关系
- **所属服务**:[[svc_sgs]] → [[svc_acquireii]](= `related_services`)。
- **读写的表**:[[tbl_acquireii_t_card_info]]。
- **配套接口**:查询 [[api_sgs_acquire_get_save_card]](解绑后查应 62078)。
- **被哪些场景测**:[[scn_online_business_direct_pay]]。

## 路径 / 方法
- 联调:`https://uat.test2pay.com/sgs/api/acquire2/removeSaveCard`;生产:`https://api.payby.com/sgs/api/acquire2/removeSaveCard`;POST(JSON)。

## 入参
bizContent = CardIndexRequest:`cardToken`(必填,需解绑的卡 token)。

## 出参
bizBody = Void(解绑成功无业务返回)。成功时 `head.applyStatus=SUCCESS`、`code=0`。

## 错误码
通用码见 [[reference_acquire_protocol_and_codes]]。特有:`62078 CARD_NOT_EXIST`(cardToken 错误或卡已解绑)。

## 测试校验点(QA)
- cardToken 缺失 → INVALID_PARAMETER;重复解绑同一 token → 第二次 62078;不存在 → 62078。
- 解绑后效果:用同 cardToken 调 [[api_sgs_acquire_get_save_card]] → 62078;用其发起支付应不可用。
- 跨商户越权:商户 A 不应能解绑商户 B 的 cardToken(应返回 CARD_NOT_EXIST 或鉴权失败)。
- 成功 body 为空(Void);`sign` 验签。
