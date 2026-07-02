---
id: tbl_campaign_t_part_in_record
object_type: Table
name: t_part_in_record (t_part_in_record)
aliases: [t_part_in_record, campaign.t_part_in_record]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: campaign schema DDL
tags: [marketing, campaign]
sensitivity: normal
related_services: []
---

# t_part_in_record (t_part_in_record)

## 用途
物理表 `campaign.t_part_in_record`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `request_no` | varchar(64) | 请求号 |
| `part_in_type` | varchar(15) | 参与类型 · 可空 |
| `partner_id` | varchar(32) | 合作方id |
| `member_id` | varchar(32) | 会员id |
| `cmpn_id` | bigint | 活动id |
| `rela_mid` | varchar(32) | 关联用户id · 可空 |
| `status` | varchar(10) | 状态 · 可空 |
| `error_code` | varchar(50) | 错误码 · 可空 |
| `error_msg` | varchar(50) | 错误信息 · 可空 |
| `utm_source` | varchar(20) | 来源 · 可空 |
| `utm_medium` | varchar(20) | 媒介 · 可空 |
| `merch_id` | bigint(32) | 商户id · 可空 |
| `store_id` | bigint | 店铺id · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
