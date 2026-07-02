---
id: tbl_sme_t_autodebit_protocol
object_type: Table
name: autodebit agreement (t_autodebit_protocol)
aliases: [t_autodebit_protocol, sme.t_autodebit_protocol]
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

# autodebit agreement (t_autodebit_protocol)

## 用途
物理表 `sme.t_autodebit_protocol`,主键 `id`。autodebit agreement。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `third_user_id` | varchar(20) | Third-party channel user id |
| `signer_id` | varchar(20) | The user id of the contracted user in payby |
| `third_party_name` | varchar(20) | User source channel name |
| `sign_order_no` | varchar(64) | The number of the business side transaction order that initiated the contract |
| `sign_order_source` | smallint | 1: t_sign_order 的sign_order_no  2: t_repay_record的repay_no |
| `apply_status` | varchar(20) | 待补 |
| `sign_time` | timestamp | Contract completion time · 可空 |
| `effect_time` | timestamp | Effective time · 可空 |
| `invalid_time` | timestamp | Failure time · 可空 |
| `protocol_status` | varchar(20) | Agreement status: EXPIRED，TERMINATED，INEFFECTIVE，EFFECTIVE · 可空 |
| `partner_id` | varchar(20) | Contracted merchant number · 可空 |
| `ext` | varchar(255) | 待补 · 可空 |
| `auth_protocol_no` | varchar(64) | Protocol number · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_no`:sign_order_no, sign_order_source (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
