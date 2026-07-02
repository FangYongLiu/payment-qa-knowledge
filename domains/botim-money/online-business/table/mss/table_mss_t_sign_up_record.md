---
id: tbl_mss_t_sign_up_record
object_type: Table
name: 报名记录【废弃】 (t_sign_up_record)
aliases: [t_sign_up_record, mss.t_sign_up_record]
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

# 报名记录【废弃】 (t_sign_up_record)

## 用途
物理表 `mss.t_sign_up_record`,主键 `sign_up_record_id`。报名记录【废弃】。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `sign_up_record_id` | bigint | 主键id |
| `activity_id` | varchar(32) | 活动id · 可空 |
| `member_id` | varchar(32) | 会员id · 可空 |
| `tool_id` | varchar(32) | 工具id · 可空 |
| `sign_up_time` | varchar(32) | 报名时间 · 可空 |
| `global_id` | varchar(32) | 订单号 · 可空 |
| `request_no` | varchar(32) | 请求号 · 可空 |
| `notice_status` | varchar(32) | 通知状态 · 可空 |
| `partner_id` | varchar(32) | 平台id · 可空 |
| `utm_source` | varchar(32) | 来源平台 · 可空 |
| `utm_medium` | varchar(32) | 来源类型 · 可空 |
| `status` | varchar(32) | 状态 · 可空 |
| `resp_code` | varchar(32) | 返回码 · 可空 |
| `error_msg` | varchar(32) | 错误信息 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `updated_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`sign_up_record_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
