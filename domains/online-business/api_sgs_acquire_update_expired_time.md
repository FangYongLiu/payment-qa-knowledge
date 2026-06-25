---
id: api_sgs_acquire_update_expired_time
object_type: API
name: 更新订单超时时间接口(acquire2/updateExpiredTime)
aliases: [updateExpiredTime]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: 接口文档
source_ref: PayBy API v2.25 p16
tags: [online-business, acquiring, SGS, 订单超时]
related_services: [svc_sgs, svc_acquireii]
related_tables: [tbl_acquireii_t_acquire_order]
related_scenarios: []
---

# 更新订单超时时间接口(acquire2/updateExpiredTime)

## 用途
调整订单过期时间。**新过期时间只能为调用接口时间往后的 15 天内**。

## 关联关系
- **所属服务**:[[svc_sgs]] → [[svc_acquireii]](= `related_services`)。
- **读写的表**:[[tbl_acquireii_t_acquire_order]]。
- **配套接口**:更新后用 [[api_sgs_acquire_get_order]] 核对 expiredTime。

## 路径 / 方法
- 联调:`https://uat.test2pay.com/sgs/api/acquire2/updateExpiredTime`;生产:`https://api.payby.com/sgs/api/acquire2/updateExpiredTime`;POST(JSON)。

## 入参
bizContent = UpdateExpiredTimeRequest:`merchantOrderNo`(商户订单号)、`expiredTime`(Timestamp(3),须在调用时间往后 15 天内)。公共 Header/Body 见 [[reference_acquire_protocol_and_codes]]。

## 出参
bizBody = GetOrderResponse:`acquireOrder`(`expiredTime` 等于入参,其他字段保持原订单)。

## 错误码
通用码见 [[reference_acquire_protocol_and_codes]]。特有:`62089 INVALID_EXPIRED_TIME`(无效超时时间)。

## 测试校验点(QA)
- expiredTime 边界:早于当前 → 62089;晚于当前+15 天 → 62089;区间内 → 成功且返回 expiredTime 等于入参。
- merchantOrderNo 须对应已存在订单;不存在/非法 → INVALID_PARAMETER。
- 其他字段(status/paymentInfo/totalAmount)保持原值;仅成功返回 body;`sign` 验签。
