---
id: tbl_mhtfundout_t_audit_data
object_type: Table
name: t_audit_data (t_audit_data)
aliases: [t_audit_data, mhtfundout.t_audit_data]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mhtfundout schema DDL
tags: [merchant-management, mhtfundout]
sensitivity: normal
related_services: []
---

# t_audit_data (t_audit_data)

## 用途
物理表 `mhtfundout.t_audit_data`,主键 `global_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 全局号 |
| `initiator_mid` | varchar(50) | 发起人会员号 · 可空 |
| `auditor_mid` | varchar(50) | 审核人员计数 · 可空 |
| `submitted_time` | timestamp(3) | 提交审核时间 · 可空 |
| `audited_time` | timestamp(3) | 审核完成时间 · 可空 |
| `audited_result` | varchar(50) | 审核结果 · 可空 |
| `audited_reason` | varchar(200) | 审核理由 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`global_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
