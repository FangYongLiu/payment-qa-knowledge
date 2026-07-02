---
id: tbl_sme_t_ad_sign_order
object_type: Table
name: Contract record (t_ad_sign_order)
aliases: [t_ad_sign_order, sme.t_ad_sign_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: sme schema DDL
tags: [lending, sme]
sensitivity: normal
related_services: []
---

# Contract record (t_ad_sign_order)

## 用途
物理表 `sme.t_ad_sign_order`,主键 `id`。Contract record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 待补 · 可空 |
| `sign_order_no` | varchar(64) | Contract order number |
| `amount` | decimal(15, 2) | amount |
| `start_time` | timestamp | When the request to payby is successfully submitted · 可空 |
| `payment_success_time` | timestamp | Payment success time · 可空 |
| `revoke_success_time` | timestamp | revoke success time after payment · 可空 |
| `payment_no` | varchar(64) | The payment order number returned by payby · 可空 |
| `finish_time` | timestamp | End time · 可空 |
| `status` | smallint | Status 0: Initial status, payby has not been submitted, 1: payby has been submitted, 2: payment succeeded, 3: refund succeeded, -2: payment failed |
| `third_user_id` | varchar(20) | Third-party channel user id |
| `third_party_name` | varchar(20) | User source channel name |
| `mobile` | varchar(32) | The phone number of the subscriber |
| `create_time` | timestamp | Creation time · 可空 |
| `update_time` | timestamp | Modification time · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
