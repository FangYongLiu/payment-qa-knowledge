---
id: tbl_mns__t_notify_msg_del
object_type: Table
name: 消息 (_t_notify_msg_del)
aliases: [_t_notify_msg_del, mns._t_notify_msg_del]
domain: infrastructure
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mns schema DDL
tags: [infrastructure, mns]
sensitivity: normal
related_services: []
---

# 消息 (_t_notify_msg_del)

## 用途
物理表 `mns._t_notify_msg_del`,主键 `msg_id`。消息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `msg_id` | bigint(18) | 消息id |
| `app_id` | varchar(64) | 应用id |
| `source` | varchar(64) | 来源 · 可空 |
| `msg_order_no` | varchar(32) | 消息发送流水号 |
| `msg_type` | varchar(1) | 消息类型 |
| `notify_type` | varchar(1) | r-实时发送 d-延时发送 |
| `subject` | varchar(256) | 主题 mail发送方式需要 · 可空 |
| `content` | text | 消息内容 · 可空 |
| `target_address` | varchar(2000) | 消息发送地址 |
| `template_no` | varchar(50) | 模板序列号 · 可空 |
| `partner_id` | varchar(22) | 平台id · 可空 |
| `gmt_pre_time` | timestamp | 预定发送时间 · 可空 |
| `status` | varchar(1) | i-初始 w-待处理 s-成功 f-失败 |
| `ip_addr` | varchar(32) | 发送ip · 可空 |
| `notify_priority` | int(2) | 优先级 · 可空 |
| `request_time` | timestamp | 消息请求时间 · 可空 |
| `deliver_time` | timestamp | 消息发出时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 |
| `gmt_create` | timestamp | 创建时间 |
| `memo` | varchar(256) | 备注 · 可空 |
| `batch_id` | int(16) | 上传批次号 · 可空 |
| `AREA_CODE` | varchar(12) | 区号 · 可空 |
| `number_of_segments` | int | 短信条数 · 可空 |
| `number_of_characters` | int | 短信字符数 · 可空 |

## 主键 / 索引
- 主键:`msg_id`
- `idx_batch_load`:gmt_pre_time, status
- `idx_nmo_order`:msg_order_no, app_id
- `idx_notify_msg_request_time`:request_time

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
