---
id: tbl_autodebit_t_ca_autodebit_protocol
object_type: Table
name: autodebit 协议 (t_ca_autodebit_protocol)
aliases: [t_ca_autodebit_protocol, autodebit.t_ca_autodebit_protocol]
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

# autodebit 协议 (t_ca_autodebit_protocol)

## 用途
物理表 `autodebit.t_ca_autodebit_protocol`,主键 `id`。autodebit 协议。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `user_id` | varchar(20) | 用户id |
| `trade_order_no` | varchar(64) | 发起签约的业务端交易订单号 |
| `apply_sign_status` | varchar(20) | 待补 |
| `sign_time` | timestamp | 签约完成时间 · 可空 |
| `effect_time` | timestamp | 生效时间 · 可空 |
| `invalid_time` | timestamp | 失效时间 · 可空 |
| `protocol_status` | varchar(20) | 协议状态 · 可空 |
| `amount` | decimal(15, 2) | 代扣时签协议金额 · 可空 |
| `product_code` | varchar(20) | 产品 · 可空 |
| `partner_id` | varchar(20) | 签约商户号 · 可空 |
| `request_no` | varchar(64) | 流水号 · 可空 |
| `ext` | varchar(255) | 额外信息 · 可空 |
| `protocol_no` | varchar(64) | 协议号 · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `idx_request_no`:request_no
- `idx_ton`:trade_order_no
- `idx_uid`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
