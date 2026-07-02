---
id: tbl_mss_t_award_item_group_relation
object_type: Table
name: 奖品和组关系 (t_award_item_group_relation)
aliases: [t_award_item_group_relation, mss.t_award_item_group_relation]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mss schema DDL
tags: [online-business, mss]
sensitivity: normal
related_services: []
---

# 奖品和组关系 (t_award_item_group_relation)

## 用途
物理表 `mss.t_award_item_group_relation`,主键 `relation_id`。奖品和组关系。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `relation_id` | int | 主键id · 可空 |
| `award_group_id` | int | 奖品组id |
| `award_item_id` | int | 奖品id |
| `award_count` | bigint | 库存 |
| `award_weight` | int | 权重 |
| `award_odds` | decimal(4, 4) | 优胜率 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`relation_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
