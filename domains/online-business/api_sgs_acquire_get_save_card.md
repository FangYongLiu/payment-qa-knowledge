---
id: api_sgs_acquire_get_save_card
object_type: API
name: 查询已保存卡信息接口(acquire2/getSaveCard)
aliases: [getSaveCard]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: 接口文档
source_ref: PayBy API v2.25 p15
tags: [online-business, acquiring, SGS, savedCard, cardToken]
related_services: [svc_sgs, svc_acquireii]
related_tables: [tbl_acquireii_t_card_info]
related_scenarios: [scn_online_business_direct_pay]
---

# 查询已保存卡信息接口(acquire2/getSaveCard)

## 用途
通过已保存的 `cardToken` 查询卡展示信息(品牌/卡类型/末四位),用于商户侧展示已保存的卡(savedCard 复用支付前)。

## 关联关系
- **所属服务**:[[svc_sgs]] → [[svc_acquireii]](= `related_services`)。
- **读写的表**:[[tbl_acquireii_t_card_info]]。
- **配套接口**:解绑 [[api_sgs_acquire_remove_save_card]](解绑后再查应返回 62078)。cardToken 由 DIRECTPAY saveCard=true 时下单返回。
- **被哪些场景测**:[[scn_online_business_direct_pay]]。

## 路径 / 方法
- 联调:`https://uat.test2pay.com/sgs/api/acquire2/getSaveCard`;生产:`https://api.payby.com/sgs/api/acquire2/getSaveCard`;POST(JSON)。

## 入参
bizContent = CardIndexRequest:`cardToken`(必填,已保存卡 token)。

## 出参
bizBody = GetSaveCardResponse:`cardInfo`(`brand` 如 MASTERCARD、`cardToken`、`cardType` 如 DC、`last4`)。

## 错误码
通用码见 [[reference_acquire_protocol_and_codes]]。特有:`62078 CARD_NOT_EXIST`(cardToken 错误或卡已解绑)。

## 测试校验点(QA)
- cardToken 缺失/格式错误 → INVALID_PARAMETER;不存在/已解绑 → 62078。
- 成功返回 cardInfo 四字段;last4 为 4 位;cardToken 与请求一致。
- 与解绑联动:[[api_sgs_acquire_remove_save_card]] 解绑后再查同 cardToken → 62078。
