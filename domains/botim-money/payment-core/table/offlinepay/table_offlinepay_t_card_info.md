---
id: tbl_offlinepay_t_card_info
object_type: Table
name: card info (t_card_info)
aliases: [t_card_info, offlinepay.t_card_info]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: offlinepay schema DDL
tags: [payment-core, offlinepay]
sensitivity: normal
related_services: []
---

# card info (t_card_info)

## 用途
物理表 `offlinepay.t_card_info`,主键 `global_id`。card info。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | global_id |
| `brand` | varchar(64) | brand · 可空 |
| `card_id` | varchar(64) | card_id · 可空 |
| `card_num_mask` | varchar(64) | card_num_mask · 可空 |
| `card_type` | varchar(8) | card_type · 可空 |
| `card_level` | varchar(16) | card_level · 可空 |
| `exp_month` | char(2) | exp_month · 可空 |
| `exp_year` | char(4) | exp_year · 可空 |
| `issue_bank` | varchar(32) | issue_bank · 可空 |
| `issue_country_code` | varchar(10) | issue_country_code · 可空 |
| `created_time` | timestamp(3) | created_time |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `data_version` | bigint | data_version |

## 主键 / 索引
- 主键:`global_id`
- `i_ci_ct`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
