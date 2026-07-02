---
id: tbl_mss_t_register_record
object_type: Table
name: 报名记录 (t_register_record)
aliases: [t_register_record, mss.t_register_record]
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

# 报名记录 (t_register_record)

## 用途
物理表 `mss.t_register_record`,主键 `register_id`。报名记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `register_id` | bigint | 主键id |
| `order_no` | bigint | 订单号 |
| `member_id` | varchar(32) | 会员号 |
| `relation_mid` | varchar(32) | 关联用户 · 可空 |
| `activity_code` | varchar(64) | 活动id |
| `notice_status` | varchar(16) | 通知状态 |
| `status` | char | 状态 |
| `error_code` | varchar(128) | 异常状态 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |
| `utm_source` | varchar(32) | 来源平台 · 可空 |
| `utm_medium` | varchar(32) | 来源类型 · 可空 |
| `register_type` | varchar(16) | 报名类型 · 可空 |
| `extension` | varchar(256) | 扩展字段 · 可空 |

## 主键 / 索引
- 主键:`register_id`
- `idx_create_time`:created_time
- `idx_member_id`:member_id
- `idx_relation_mid`:relation_mid
- `idx_sign_order`:order_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
