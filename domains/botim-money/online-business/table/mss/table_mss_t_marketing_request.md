---
id: tbl_mss_t_marketing_request
object_type: Table
name: 营销请求记录 (t_marketing_request)
aliases: [t_marketing_request, mss.t_marketing_request]
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

# 营销请求记录 (t_marketing_request)

## 用途
物理表 `mss.t_marketing_request`,主键 `request_id`。营销请求记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `request_id` | bigint | 主键ID |
| `request_no` | varchar(64) | 请求号 用户标识唯一一次请求 |
| `marketing_scenes` | varchar(32) | 营销场景 |
| `request_source` | varchar(32) | 来源 |
| `biz_message` | varchar(4096) | 请求业务参数 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`request_id`
- `uk_reqno_scenes`:request_no, marketing_scenes (UNIQUE)
- `idx_scenes_mid`:marketing_scenes, request_source

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
