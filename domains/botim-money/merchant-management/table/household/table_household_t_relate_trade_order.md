---
id: tbl_household_t_relate_trade_order
object_type: Table
name: t_relate_trade_order (t_relate_trade_order)
aliases: [t_relate_trade_order, household.t_relate_trade_order]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: household schema DDL
tags: [merchant-management, household]
sensitivity: normal
related_services: []
---

# t_relate_trade_order (t_relate_trade_order)

## 用途
物理表 `household.t_relate_trade_order`,主键 `request_no`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `request_no` | bigint | Request No: Trade request no or Refund request no |
| `trade_source` | varchar(16) | Trade Source: TransferOrder,TransferReceive |
| `trade_type` | varchar(8) | Trade Type: Trade,Refund |
| `trade_status` | varchar(16) | Status: Processing,Failure,Success |
| `relate_id` | bigint | Relate ID |
| `unity_result_code` | varchar(100) | Unity Result Code · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`request_no`
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
