---
id: tbl_mss_t_award_item
object_type: Table
name: 奖品 (t_award_item)
aliases: [t_award_item, mss.t_award_item]
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

# 奖品 (t_award_item)

## 用途
物理表 `mss.t_award_item`,主键 `award_item_id`。奖品。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `award_item_id` | int | 主键id · 可空 |
| `award_type` | varchar(16) | 奖品类型 实物，现金，优惠券 |
| `award_sub_type` | varchar(16) | 奖品子类型 |
| `award_attr` | char(4) | 奖品属性（叠加后单张） · 可空 |
| `award_no` | varchar(32) | 奖品编号 |
| `award_name` | varchar(64) | 奖品名称 |
| `show_name` | varchar(64) | 管理后台展示名称 · 可空 |
| `resource_url` | varchar(512) | 实物奖品资源url · 可空 |
| `detail_url` | varchar(512) | 奖品详情地址 · 可空 |
| `use_url` | varchar(512) | 奖品使用地址 · 可空 |
| `par_value` | decimal(12, 4) | 默认面额 固定额度优惠券，现金类必须 · 可空 |
| `discount_percent` | decimal(4, 2) | 默认折扣 固定额度优惠券，现金类必须 · 可空 |
| `discount_limit` | decimal(8, 4) | 折扣金额上限 · 可空 |
| `max_random_amount` | varchar(32) | 最大随机额度 随机奖品必须 · 可空 |
| `min_random_amount` | varchar(32) | 最小随机额度 随机奖品必须 · 可空 |
| `currency` | char(3) | 币种 |
| `status` | char | 状态 |
| `description` | varchar(512) | 奖品描述 · 可空 |
| `memo` | varchar(512) | 备注 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`award_item_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
