---
id: tbl_mchtsettle_t_channel_summary
object_type: Table
name: channel summary (t_channel_summary)
aliases: [t_channel_summary, mchtsettle.t_channel_summary]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mchtsettle schema DDL
tags: [online-business, mchtsettle]
sensitivity: normal
related_services: [svc_merchant_settlement]
---

# channel summary (t_channel_summary)

## 用途
物理表 `mchtsettle.t_channel_summary`,主键 `id`。channel summary。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 待补 |
| `count` | bigint | count |
| `batch_id` | bigint | batch id |
| `card_type` | varchar(16) | card type |
| `amount` | decimal(19, 4) | positive:fundin,degative:foudout · 可空 |
| `currency` | char(3) | currency · 可空 |
| `status` | varchar(20) | status |
| `created_time` | timestamp(3) | created time |
| `last_updated_time` | timestamp(3) | last updated time |
| `data_version` | bigint | data version |

## 主键 / 索引
- 主键:`id`
- `uk_cs_card`:batch_id, card_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
