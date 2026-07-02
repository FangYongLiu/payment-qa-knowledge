---
id: api_sgs_transfer_place_order
object_type: API
name: 单笔付款到账户接口(transfer/placeTransferOrder + getTransferOrder)
aliases: [placeTransferOrder, getTransferOrder, transfer to account]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: 接口文档
source_ref: PayBy API v2.25 p13
tags: [online-business, transfer, payout, SGS]
related_services: [svc_sgs, svc_merchant_fundout, svc_fundout]
related_tables: []
related_scenarios: [scn_online_business_merchant_payout]
---

# 单笔付款到账户接口(transfer/placeTransferOrder + getTransferOrder)

## 用途
企业付款到用户账户:向个人手机号或企业会员 ID 发起单笔转账(placeTransferOrder),并通过查询接口(getTransferOrder)获取付款最终结果。

## 关联关系
- **所属服务**:接入网关 [[svc_sgs]] → 出款 [[svc_merchant_fundout]] / [[svc_fundout]](= `related_services`)。
- **被哪些场景测**:[[scn_online_business_merchant_payout]] 商户出款/转账。
- **落库表**:待补(出款单表,QA 视角需补 fundout 库表对象)。

## 路径 / 方法
- **下单 placeTransferOrder**:联调 `https://uat.test2pay.com/sgs/api/transfer/placeTransferOrder`;生产 `https://api.payby.com/sgs/api/transfer/placeTransferOrder`。
- **查询 getTransferOrder**:联调 `https://uat.test2pay.com/sgs/api/transfer/getTransferOrder`;生产 `https://api.payby.com/sgs/api/transfer/getTransferOrder`。
- 方法:POST(JSON)。公共 Header/Body 见 [[reference_acquire_protocol_and_codes]]。

## 入参
### 下单 PlaceTransferOrderRequest
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| merchantOrderNo | String(64) | Y | 商户订单号 |
| beneficiaryIdentityType | enum | Y | `PHONE_NO`(个人)/ `MEMBER_ID`(企业) |
| beneficiaryIdentity | String | Y | 用户标识,**加密传输**;PHONE_NO 带区号(如 `971-585812345`) |
| beneficiaryFullName | String(100) | N | 收款人姓名,加密;上传则强制校验姓名 |
| amount | Money | Y | 金额 |
| memo | String(128) | Y | 企业付款备注 |
| notifyUrl | String | N | 后端通知地址 |

### 查询 GetTransferOrderRequest
- `merchantOrderNo`(必填)。

## 出参
两接口均返回 `transferOrder`(TransferOrder):orderNo、merchantOrderNo、收款方信息(加密返回)、amount、memo、notifyUrl、product(`Transfer`)、requestTime、`status`(CREATED/SUCCESS/FAILURE)、`paymentInfo`(arrivalTime 到账时间、payerFeeAmount 付款方手续费)。

### 状态机
| Status | 说明 |
| --- | --- |
| CREATED | 已创建 |
| SUCCESS | 已成功 |
| FAILURE | 已失败 |

## 错误码
通用码见 [[reference_acquire_protocol_and_codes]]。下单特有:`62002 ORDER_FAILURE`、`62016 MERCHANT_ORDER_NO_EXIST`、`62020 PAYERMID_PAYEEMID_ARE_SAME`、`62023 NAME_NOT_MATCH`、`62026 PRODUCT_IS_NOT_APPLIED`、`62027 BENEFICIARY_NOT_EXIST`、`62028 ORDER_SUCCESS`、`62029 ORDER_CREATED`。查询特有:`62004 MERCHANT_ORDER_NO_NOT_EXIST`。

## 测试校验点(QA)
- beneficiaryIdentityType 与 identity 匹配(PHONE_NO 带区号 / MEMBER_ID);收款人不存在 → 62027。
- beneficiaryFullName 传则强制校验,不符 → 62023。
- 同单号不同参数 → 62016;已成功/已创建再下单 → 62028/62029;付款人=收款人 → 62020。
- 查询不存在订单 → 62004;status 流转 CREATED→SUCCESS/FAILURE;paymentInfo.arrivalTime/payerFeeAmount。
- 加密字段(beneficiaryIdentity/Name)不得明文。
