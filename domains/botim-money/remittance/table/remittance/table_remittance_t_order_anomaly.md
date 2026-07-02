---
id: tbl_remittance_t_order_anomaly
object_type: Table
name: Order anomaly tracking table (t_order_anomaly)
aliases: [t_order_anomaly, remittance.t_order_anomaly]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: remittance schema DDL
tags: [remittance, remittance]
sensitivity: normal
related_services: []
---

# Order anomaly tracking table (t_order_anomaly)

## 用途
物理表 `remittance.t_order_anomaly`,主键 `id`。Order anomaly tracking table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | Primary key · 可空 |
| `order_no` | bigint | Order number |
| `anomaly_type` | varchar(32) | Anomaly type: ORDER_NOT_FOUND, ROUTER_UNDEFINED, ... |
| `channel_code` | varchar(32) | Channel code |
| `channel_order_no` | varchar(64) | Channel order number · 可空 |
| `transaction_mode` | varchar(16) | Transaction mode: C2C, B2C, etc. · 可空 |
| `order_create_time` | timestamp | Order create time from t_order · 可空 |
| `error_code` | varchar(64) | Error code · 可空 |
| `error_sub_code` | varchar(64) | Error sub code · 可空 |
| `error_message` | varchar(256) | Error message · 可空 |
| `status` | varchar(20) | Status: PENDING, RESOLVED, AUTO_RESOLVED, IGNORED |
| `remark` | varchar(255) | Remark · 可空 |
| `operator_name` | varchar(64) | Operator name · 可空 |
| `resolved_time` | timestamp | Resolved time · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`id`
- `idx_channel_order_no`:channel_order_no
- `idx_create_time`:create_time
- `idx_order_create_time`:order_create_time
- `idx_order_no`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
