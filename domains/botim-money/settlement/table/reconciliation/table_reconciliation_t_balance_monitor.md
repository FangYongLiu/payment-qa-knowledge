---
id: tbl_reconciliation_t_balance_monitor
object_type: Table
name: Balance Monitor Table (t_balance_monitor)
aliases: [t_balance_monitor, reconciliation.t_balance_monitor]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# Balance Monitor Table (t_balance_monitor)

## 用途
物理表 `reconciliation.t_balance_monitor`,主键 `monitor_id`。Balance Monitor Table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `monitor_id` | int | ID · 可空 |
| `monitor_name` | varchar(32) | Monitor Name |
| `bank_code` | varchar(32) | Bank Code |
| `channel_code` | varchar(32) | Channel Code |
| `account_type` | varchar(32) | Account Type |
| `account_no` | varchar(64) | Account No |
| `currency` | char(3) | Currency |
| `monitor_threshold` | decimal(19, 4) | Monitor Threshold |
| `alert_threshold` | decimal(19, 4) | Alert Threshold · 可空 |
| `current_version_id` | bigint | Current Version · 可空 |
| `enable_flag` | char | Enable Flag：Y=Enable，N=Disable |
| `sync_interval` | int(10) | Synchronization Interval; |
| `trigger_cron` | varchar(32) | Schedule Cron · 可空 |
| `error_message` | varchar(512) | Error Message · 可空 |
| `sync_time` | timestamp | Sync Time · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(512) | Memo · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |

## 主键 / 索引
- 主键:`monitor_id`
- `uk_name`:monitor_name (UNIQUE)
- `uk_type_bank_type_account`:bank_code, account_type, account_no (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
