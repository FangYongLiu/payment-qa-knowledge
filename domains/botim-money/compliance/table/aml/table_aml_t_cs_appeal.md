---
id: tbl_aml_t_cs_appeal
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: aml schema DDL
tags:
- aml
- t_cs_appeal
subdomain: aml
module: null
sensitivity: normal
name: 客服申诉表 (t_cs_appeal)
aliases:
- t_cs_appeal
- aml.t_cs_appeal
related_services: []
---

# 客服申诉表 (t_cs_appeal)

## 用途
物理表 `aml.t_cs_appeal`,主键 `id`。CS Appeal Table。属 AML/合规库 `aml`。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补(compliance 域 AML 服务)。
- **谁读写它**:AML/风控链路的服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `apply_id` | varchar(32) | Appeal ID |
| `payment_order_no` | varchar(64) | Payment order number · 可空 |
| `transaction_id` | varchar(64) | Transaction ID · 可空 |
| `member_id` | varchar(20) | Member ID |
| `operator` | varchar(64) | Operator (CS agent) |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`id`
- `uk_apply_id`:apply_id (UNIQUE)
- `idx_member_id`:member_id
- `idx_payment_order_no`:payment_order_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:`create_time`/`update_time`;按时间过滤走对应索引。
- **关联交易**:`payment_order_no` 关联支付订单(风控/合规按订单聚合)。
- **会员维度**:`member_id` 关联会员,风控/AML 按会员聚合。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
