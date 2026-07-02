---
id: tbl_benefit_t_benefit_earnings_detail
object_type: Table
name: t_benefit_earnings_detail (t_benefit_earnings_detail)
aliases: [t_benefit_earnings_detail, benefit.t_benefit_earnings_detail]
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

# t_benefit_earnings_detail (t_benefit_earnings_detail)

## 用途
物理表 `benefit.t_benefit_earnings_detail`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 自增id · 可空 |
| `partner_id` | varchar(32) | 合作方id |
| `member_id` | varchar(32) | 会员id |
| `shares` | decimal(19, 4) | 产生收益时的份额 · 可空 |
| `earnings_amount` | decimal(19, 4) | 收益金额 · 可空 |
| `currency` | varchar(3) | 收益金额币种 · 可空 |
| `rate` | decimal(19, 4) | 万份日收益率 · 可空 |
| `earnings_date` | date | 收益日期 |
| `status` | varchar(10) | INIT PROCESS SUCCESS CANCEL · 可空 |
| `retry_count` | tinyint | 重试次数 · 可空 |
| `next_retry_time` | timestamp | 下次重试时间 · 可空 |
| `sub_status` | varchar(10) | P S F  E · 可空 |
| `result_code` | varchar(50) | 结果码 · 可空 |
| `result_msg` | varchar(255) | 结果信息 · 可空 |
| `trial_earnings` | decimal(19, 4) | 体验金收益 · 可空 |
| `trial_amount` | decimal(19, 4) | 体验金金额 · 可空 |
| `trial_shares` | decimal(19, 4) | 体验金份额 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `idx_member_date`:member_id, earnings_date (UNIQUE)
- `idx_create_time_status`:create_time, sub_status
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
