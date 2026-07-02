---
id: tbl_transfer_t_retry_job
object_type: Table
name: t_retry_job (t_retry_job)
aliases: [t_retry_job, transfer.t_retry_job]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: transfer schema DDL
tags: [wallet, transfer]
sensitivity: normal
related_services: []
---

# t_retry_job (t_retry_job)

## 用途
物理表 `transfer.t_retry_job`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 待补 |
| `type` | varchar(20) | 类型 |
| `foreign_key` | varchar(32) | 关联Key |
| `retry_flag` | tinyint | 重试标识 1:需要 0:不需要 |
| `retried_count` | tinyint | 已重试次数 |
| `next_retry_time` | timestamp | 下次重试时间 |
| `rules` | varchar(50) | 重试规则 10m,1h,3h |
| `status` | varchar(4) | 状态, E: EXECUTING, S: SUCCESS, F: FAILED |
| `client_id` | varchar(32) | 客户端ID |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `idx_job_next_retry_time`:next_retry_time

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
