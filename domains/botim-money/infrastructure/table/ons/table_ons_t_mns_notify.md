---
id: tbl_ons_t_mns_notify
object_type: Table
name: 短信和邮件通知 (t_mns_notify)
aliases: [t_mns_notify, ons.t_mns_notify]
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

# 短信和邮件通知 (t_mns_notify)

## 用途
物理表 `ons.t_mns_notify`,主键 `id`。短信和邮件通知。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `bill_id` | varchar(128) | 账单id：账单id |
| `voucher_no` | varchar(32) | 凭证号：订单号 |
| `event_code` | varchar(32) | 通知事件 · 可空 |
| `notify_target` | varchar(128) | 通知目标：通知目标 |
| `notify_type` | varchar(10) | 通知类型：M=邮件，S=短信 |
| `template_id` | varchar(32) | 通知模板id：通知模板 · 可空 |
| `view_code` | varchar(32) | 视图编码：账单中视图编码 |
| `status` | char | 通知状态：P处理中，S成，F失败 |
| `extension` | varchar(255) | 扩展字段：扩展字段 · 可空 |
| `create_time` | timestamp | 创建时间：创建时间 |
| `update_time` | timestamp | 修改时间：修改时间 |

## 主键 / 索引
- 主键:`id`
- `uk_voucher_event_target`:voucher_no, event_code, notify_target (UNIQUE)
- `idx_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
