---
id: tbl_benefit_t_benefit_shares_change
object_type: Table
name: t_benefit_shares_change (t_benefit_shares_change)
aliases: [t_benefit_shares_change, benefit.t_benefit_shares_change]
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

# t_benefit_shares_change (t_benefit_shares_change)

## 用途
物理表 `benefit.t_benefit_shares_change`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 自增id · 可空 |
| `member_id` | varchar(32) | 会员id |
| `shares` | decimal(19, 4) | 份额变化 |
| `before_shares` | decimal(19, 4) | 变化前份额 |
| `after_shares` | decimal(19, 4) | 变化后份额 |
| `direction` | int | 1 收入 2 支出 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `idx_member_id`:member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
