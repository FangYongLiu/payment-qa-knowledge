---
id: tbl_credit_t_cs_deeplink
object_type: Table
name: deeplink record table (t_cs_deeplink)
aliases: [t_cs_deeplink, credit.t_cs_deeplink]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# deeplink record table (t_cs_deeplink)

## 用途
物理表 `credit.t_cs_deeplink`,主键 `id`。deeplink record table。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(11) | 待补 · 可空 |
| `user_id` | varchar(32) | user id |
| `deeplink` | varchar(120) | related deeplink |
| `link_channel` | varchar(16) | deeplink channel |
| `product_codes` | varchar(50) | related product codes |
| `link_time` | timestamp | user login time by deeplink |
| `user_type` | varchar(10) | user type when linked: unknown, new_new, new_again, renewal |
| `status` | smallint(5) | deeplink status 1: valid -1: invalid |
| `create_time` | timestamp | create time · 可空 |
| `update_time` | timestamp | update time · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_link_time`:link_time
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
