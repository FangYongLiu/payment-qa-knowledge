---
id: tbl_autodebit_t_ca_order
object_type: Table
name: autodebit (t_ca_order)
aliases: [t_ca_order, autodebit.t_ca_order]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: autodebit schema DDL
tags: [wallet, autodebit]
sensitivity: normal
related_services: []
---

# autodebit (t_ca_order)

## 用途
物理表 `autodebit.t_ca_order`,主键 `id`。autodebit。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `user_id` | varchar(20) | 用户id付款方 |
| `trade_order_no` | varchar(64) | 代扣订单号 |
| `status` | varchar(20) | 待补 |
| `finished_time` | timestamp | 完成时间 · 可空 |
| `amount` | decimal(15, 2) | 代扣时签协议金额 · 可空 |
| `product_code` | varchar(20) | 产品 · 可空 |
| `request_no` | varchar(64) | 流水号 · 可空 |
| `client_id` | varchar(64) | 客户ID · 可空 |
| `out_order_no` | varchar(64) | 外部ID · 可空 |
| `partner_id` | varchar(20) | 签约商户号 · 可空 |
| `ext` | varchar(255) | 额外信息 · 可空 |
| `protocol_no` | varchar(64) | 协议号 · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `idx_out_order_no`:out_order_no
- `idx_request_no`:request_no
- `idx_ton`:trade_order_no
- `idx_uid`:user_id
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
