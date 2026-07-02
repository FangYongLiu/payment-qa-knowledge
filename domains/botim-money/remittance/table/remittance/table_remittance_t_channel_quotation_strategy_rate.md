---
id: tbl_remittance_t_channel_quotation_strategy_rate
object_type: Table
name: channel quotation strategy rate extension table (t_channel_quotation_strategy_rate)
aliases: [t_channel_quotation_strategy_rate, remittance.t_channel_quotation_strategy_rate]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: remittance schema DDL
tags: [remittance, remittance]
sensitivity: normal
related_services: []
---

# channel quotation strategy rate extension table (t_channel_quotation_strategy_rate)

## 用途
物理表 `remittance.t_channel_quotation_strategy_rate`,主键 `id`。channel quotation strategy rate extension table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | primary key · 可空 |
| `strategy_id` | bigint | associated strategy id |
| `rate_id` | varchar(32) | rate id |
| `source_rate` | decimal(15, 6) | source rate |
| `source_currency` | varchar(7) | source currency |
| `aed_rate` | decimal(15, 6) | AED rate |
| `effective_time` | timestamp | effective time |
| `expire_time` | timestamp | expire time |
| `ahead_minutes` | tinyint | minutes to expire ahead |
| `create_time` | timestamp | create time |
| `update_time` | timestamp | update time |

## 主键 / 索引
- 主键:`id`
- `uk_strategy_id`:strategy_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
