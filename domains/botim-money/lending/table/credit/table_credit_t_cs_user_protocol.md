---
id: tbl_credit_t_cs_user_protocol
object_type: Table
name: 用户协议 (t_cs_user_protocol)
aliases: [t_cs_user_protocol, credit.t_cs_user_protocol]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# 用户协议 (t_cs_user_protocol)

## 用途
物理表 `credit.t_cs_user_protocol`,主键 `id`。用户协议。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `status` | tinyint(5) | 状态: 0 已申请，待签 1  已签 |
| `merchant_id` | varchar(64) | 签属商户号 · 可空 |
| `partner_id` | varchar(64) | 用户平台 · 可空 |
| `screen` | varchar(64) | 场景 · 可空 |
| `product` | varchar(64) | 产品:cashnow or paylater · 可空 |
| `voucher_no` | varchar(64) | 凭证号 |
| `protocol_no` | varchar(64) | 协议号 · 可空 |
| `user_id` | varchar(32) | 用户ID |
| `created_time` | timestamp | 创建日期 · 可空 |
| `last_modified` | timestamp | 修改日期 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
