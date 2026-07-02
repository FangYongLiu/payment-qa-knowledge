---
id: tbl_sme_t_pay_key_config
object_type: Table
name: The key information of the merchant recorded in each payment platform (t_pay_key_config)
aliases: [t_pay_key_config, sme.t_pay_key_config]
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

# The key information of the merchant recorded in each payment platform (t_pay_key_config)

## 用途
物理表 `sme.t_pay_key_config`,主键 `id`。The key information of the merchant recorded in each payment platform。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `merchant_id` | varchar(32) | We memberId in this payment platform |
| `merchant_desc` | varchar(32) | Merchant description |
| `pub_key` | varchar(512) | Public key |
| `pri_key` | varchar(1800) | Private key |
| `algorithm` | varchar(20) | Algorithm for generating the secret key · 可空 |
| `expired_time` | timestamp | Expiration time · 可空 |
| `status` | smallint | 待补 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |
| `payby_pub_key` | varchar(512) | 待补 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
