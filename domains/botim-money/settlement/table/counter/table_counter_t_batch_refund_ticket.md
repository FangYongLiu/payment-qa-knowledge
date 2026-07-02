---
id: tbl_counter_t_batch_refund_ticket
object_type: Table
name: 批量退票申请表 (t_batch_refund_ticket)
aliases: [t_batch_refund_ticket, counter.t_batch_refund_ticket]
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

# 批量退票申请表 (t_batch_refund_ticket)

## 用途
物理表 `counter.t_batch_refund_ticket`,主键 `batch_id`。批量退票申请表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `batch_id` | bigint | ID |
| `refund_date` | date | 退票日期 |
| `audit_id` | bigint | 审批id |
| `total_record` | int | 退票笔数 |
| `total_amount` | decimal(15, 2) | 退票总金额 |
| `currency` | char(3) | 币种 · 可空 |
| `file_name` | varchar(255) | 附件名称 · 可空 |
| `operator` | varchar(32) | 操作人 |
| `status` | char | 状态 W待处理，A待审核，P审核通过，D审核拒绝 |
| `result_message` | varchar(255) | 响应信息 · 可空 |
| `memo` | varchar(1024) | 备注 · 可空 |
| `extension` | varchar(255) | 扩展字段 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`batch_id`
- `idx_audit_id`:audit_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
