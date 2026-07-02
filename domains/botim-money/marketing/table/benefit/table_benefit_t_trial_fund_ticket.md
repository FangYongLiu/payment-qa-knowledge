---
id: tbl_benefit_t_trial_fund_ticket
object_type: Table
name: t_trial_fund_ticket (t_trial_fund_ticket)
aliases: [t_trial_fund_ticket, benefit.t_trial_fund_ticket]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: benefit schema DDL
tags: [marketing, benefit]
sensitivity: normal
related_services: []
---

# t_trial_fund_ticket (t_trial_fund_ticket)

## 用途
物理表 `benefit.t_trial_fund_ticket`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 自增主键 · 可空 |
| `trial_fund_code` | varchar(50) | 体验金代码 · 可空 |
| `trial_amount` | decimal(19, 4) | 体验金金额 |
| `currency` | char(3) | 币种 |
| `trial_days` | int | 体验天数 |
| `status` | tinyint(1) | 状态 0:无效  1:有效 |
| `activate_limit_days` | int | 限时激活天数 · 可空 |
| `start_time` | timestamp | 开始时间 |
| `end_time` | timestamp | 结束时间 |
| `white_list_key` | varchar(50) | 白名单key · 可空 |
| `total_count` | bigint | 体验金总数 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
