---
id: tbl_ppc_t_corporation_fee_order
object_type: Table
name: Corporation Fee Order (t_corporation_fee_order)
aliases: [t_corporation_fee_order, ppc.t_corporation_fee_order]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# Corporation Fee Order (t_corporation_fee_order)

## 用途
物理表 `ppc.t_corporation_fee_order`,主键 `fee_order_no`。Corporation Fee Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `fee_order_no` | bigint | Fee Order No |
| `request_order_no` | varchar(32) | Request Order No |
| `corporation_id` | varchar(50) | Corporation ID |
| `fee_type` | varchar(8) | Fee Type: BDF=Bulk Delivery Fee, CC=Close Card |
| `fee_amount` | decimal(19, 4) | Fee Amount |
| `currency` | char(3) | Currency |
| `status` | varchar(1) | Status: C=Created, F=Failed, S=Succeed, R=Retry |
| `trade_request_no` | bigint | Trade Request Number · 可空 |
| `unity_result_code` | varchar(50) | Unity Result Code · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`fee_order_no`
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
