---
id: tbl_benefit_t_benefit_account
object_type: Table
name: t_benefit_account (t_benefit_account)
aliases: [t_benefit_account, benefit.t_benefit_account]
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

# t_benefit_account (t_benefit_account)

## 用途
物理表 `benefit.t_benefit_account`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 自增id · 可空 |
| `partner_id` | varchar(32) | 合作方id · 可空 |
| `member_id` | varchar(32) | 会员id |
| `shares` | decimal(19, 4) | 余额宝份额 · 可空 |
| `earnings` | decimal(19, 4) | 持有收益 · 可空 |
| `currency` | varchar(3) | 币种 · 可空 |
| `status` | varchar(10) | 状态 OPEN:开通 CLOSE:关闭 · 可空 |
| `total_earnings` | decimal(19, 4) | 累计总收益 · 可空 |
| `total_trial_earnings` | decimal(19, 4) | 累计体验金收益 · 可空 |
| `protocol_no` | varchar(32) | 协议流水号 · 可空 |
| `earnings_flag` | int(8) | 收益标记，默认为0 收益计算后更新为收益日期 |
| `open_time` | timestamp | 开通时间 |
| `close_time` | timestamp | 关闭时间 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `idx_member_id`:member_id (UNIQUE)
- `idx_close_time`:close_time
- `idx_earnings_flag`:earnings_flag
- `idx_open_time`:open_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
