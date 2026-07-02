---
id: tbl_basicrcdata_t_leantech_loan_limit
object_type: Table
name: t_leantech_loan_limit (t_leantech_loan_limit)
aliases: [t_leantech_loan_limit, basicrcdata.t_leantech_loan_limit]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basicrcdata schema DDL
tags: [risk, basicrcdata]
sensitivity: normal
related_services: []
---

# t_leantech_loan_limit (t_leantech_loan_limit)

## 用途
物理表 `basicrcdata.t_leantech_loan_limit`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `salary_lower` | decimal(18, 4) | 薪水下限 |
| `salary_upper` | decimal(18, 4) | 薪水上限 |
| `income_month_cnt_lower` | int | 连续收入月份下限 |
| `income_month_cnt_upper` | int | 连续收入月份上限 |
| `rating` | varchar(10) | 信用等级 |
| `multiplier` | decimal(10, 4) | 工资额度乘数 |
| `term` | int | 分期期数 |
| `fee_rate` | decimal(10, 4) | 费率 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
