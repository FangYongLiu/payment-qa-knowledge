---
id: tbl_aml_t_member_limit_inv_prod
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
- t_member_limit_inv_prod
subdomain: aml
module: null
sensitivity: normal
name: 理财产品限额表 (t_member_limit_inv_prod)
aliases:
- t_member_limit_inv_prod
- aml.t_member_limit_inv_prod
related_services: []
---

# 理财产品限额表 (t_member_limit_inv_prod)

## 用途
物理表 `aml.t_member_limit_inv_prod`,主键 `id`。investments product limit table。属 AML/合规库 `aml`。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补(compliance 域 AML 服务)。
- **谁读写它**:AML/风控链路的服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | ID · 可空 |
| `payment_order_no` | varchar(64) | Payment Order No · 可空 |
| `member_id` | varchar(20) | Member Id · 可空 |
| `id_no` | varchar(32) | Id No · 可空 |
| `order_amount` | decimal(15, 4) | Order Amount · 可空 |
| `add_limit_amount` | decimal(15, 4) | Add Limit Amount · 可空 |
| `currency` | char(3) | Currency · 可空 |
| `data_type` | varchar(20) | Data Type (order/roll_over) · 可空 |
| `status` | varchar(10) | status · 可空 |
| `extension` | varchar(200) | extension · 可空 |
| `create_time` | timestamp(3) | Create Time · 可空 |
| `update_time` | timestamp(3) | Update Time · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_create_time`:create_time
- `idx_member_id`:member_id
- `idx_paymentOrderNo`:payment_order_no

## 校验点(QA 关注)
- **时间字段**:`create_time`/`update_time`;按时间过滤走对应索引。
- **状态字段**:合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 金额比较用容差(< 0.01);amount 与 currency 需一致。
- **关联交易**:`payment_order_no` 关联支付订单(风控/合规按订单聚合)。
- **会员维度**:`member_id` 关联会员,风控/AML 按会员聚合。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
