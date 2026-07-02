---
id: tbl_counter_t_batch_bank_flow
object_type: Table
name: 批量线下入金 (t_batch_bank_flow)
aliases: [t_batch_bank_flow, counter.t_batch_bank_flow]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# 批量线下入金 (t_batch_bank_flow)

## 用途
物理表 `counter.t_batch_bank_flow`,主键 `batch_id`。批量线下入金。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `batch_id` | bigint(17) | 批次ID |
| `batch_no` | varchar(64) | 批次号 |
| `batch_date` | timestamp | 批次日期 · 可空 |
| `batch_type` | varchar(4) | 批次类型 FABPayroll · 可空 |
| `status` | varchar(4) | 状态 见状态机 · 可空 |
| `file_name` | varchar(255) | 文件名 · 可空 |
| `ufs_name` | varchar(255) | ufs文件名 · 可空 |
| `total_num` | int | 总笔数 · 可空 |
| `total_amount` | decimal(15, 2) | 总金额 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `operator` | varchar(64) | 操作者 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |
| `result_msg` | varchar(1024) | 解析结果,解析失败原因 · 可空 |

## 主键 / 索引
- 主键:`batch_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
