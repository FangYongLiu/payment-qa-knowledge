---
id: tbl_ccdpm_t_dpm_outer_account_status_his
object_type: Table
name: 外部账户状态历史 (t_dpm_outer_account_status_his)
aliases: [t_dpm_outer_account_status_his, ccdpm.t_dpm_outer_account_status_his]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccdpm schema DDL
tags: [crypto, ccdpm]
sensitivity: normal
related_services: []
---

# 外部账户状态历史 (t_dpm_outer_account_status_his)

## 用途
物理表 `ccdpm.t_dpm_outer_account_status_his`,主键 `his_id`。外部账户状态历史。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `his_id` | bigint | 历史ID |
| `account_no` | varchar(32) | 账户号 |
| `status_map` | varchar(6) | 状态 |
| `pre_status_map` | varchar(6) | 变更前状态 · 可空 |
| `update_time` | timestamp | 变更时间 · 可空 |
| `update_user` | varchar(128) | 变更人 · 可空 |
| `memo` | varchar(256) | 备注 · 可空 |
| `client_id` | varchar(32) | 调用方 · 可空 |

## 主键 / 索引
- 主键:`his_id`
- `idx_account_status_his_account_no`:account_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
