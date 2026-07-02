---
id: tbl_ons_t_official_notify
object_type: Table
name: 公众号通知 (t_official_notify)
aliases: [t_official_notify, ons.t_official_notify]
domain: infrastructure
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ons schema DDL
tags: [infrastructure, ons]
sensitivity: normal
related_services: []
---

# 公众号通知 (t_official_notify)

## 用途
物理表 `ons.t_official_notify`,主键 `id`。公众号通知。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `bill_id` | varchar(128) | 账单id |
| `voucher_no` | varchar(32) | 凭证号 |
| `event_code` | varchar(32) | 通知类型 |
| `notify_partner_id` | varchar(32) | 通知平台 |
| `view_code` | varchar(32) | 视图编码 |
| `status` | char | 通知状态：P处理中，S成，F失败 |
| `extension` | varchar(255) | 扩展字段：扩展字段 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `uk_billid_event_partner`:bill_id, event_code, notify_partner_id (UNIQUE)
- `idx_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
