---
id: tbl_ppc_t_relate_trade_order
object_type: Table
name: Relate Trade Order (t_relate_trade_order)
aliases: [t_relate_trade_order, ppc.t_relate_trade_order]
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

# Relate Trade Order (t_relate_trade_order)

## 用途
物理表 `ppc.t_relate_trade_order`,主键 `trade_request_no`。Relate Trade Order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `trade_request_no` | bigint | Trade Request No |
| `order_type` | char(8) | Order Type: CF=Corp Fee |
| `order_voucher_no` | bigint | Order Voucher No |
| `trade_status` | char | Trade Status: P-Processing, F-Failure, S-Success |
| `extension` | varchar(128) | Extension · 可空 |
| `unity_result_code` | varchar(50) | Unity Result Code · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`trade_request_no`
- `idx_order_voucher_no`:order_voucher_no
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
