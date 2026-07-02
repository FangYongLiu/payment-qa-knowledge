---
id: tbl_mhtfundout_t_withdraw_prerequisite
object_type: Table
name: 提现先决条件 (t_withdraw_prerequisite)
aliases: [t_withdraw_prerequisite, mhtfundout.t_withdraw_prerequisite]
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

# 提现先决条件 (t_withdraw_prerequisite)

## 用途
物理表 `mhtfundout.t_withdraw_prerequisite`,主键 `id`。提现先决条件。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `source` | varchar(50) | 币种来源 |
| `target` | varchar(50) | 币种去向 |
| `withdraw_usage` | varchar(50) | 用途 |
| `minimum_source_amount` | decimal(19, 4) | 最小来源金额 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `uk_wp_stu`:source, target, withdraw_usage (UNIQUE)
- `i_wo_ct`:withdraw_usage
- `i_wo_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
