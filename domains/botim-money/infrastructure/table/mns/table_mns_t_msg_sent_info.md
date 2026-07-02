---
id: tbl_mns_t_msg_sent_info
object_type: Table
name: 消息发送信息表 (t_msg_sent_info)
aliases: [t_msg_sent_info, mns.t_msg_sent_info]
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

# 消息发送信息表 (t_msg_sent_info)

## 用途
物理表 `mns.t_msg_sent_info`,主键 `id`。消息发送信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键id |
| `msg_id` | bigint(18) | 消息id |
| `channel` | varchar(32) | 渠道名 · 可空 |
| `channel_id` | bigint(16) | 消息id |
| `status_msg_id` | varchar(64) | 待补 · 可空 |
| `connect_info` | varchar(800) | 链接信息 · 可空 |
| `gmt_modified` | timestamp | 修改时间 |
| `gmt_create` | timestamp | 创建时间 |
| `memo` | varchar(128) | 备注 · 可空 |
| `SUPPLIER` | varchar(18) | 供应商 · 可空 |
| `ERROR_UNIT_CODE` | varchar(32) | 错误码 · 可空 |
| `ERROR_MESSAGE` | varchar(255) | 供应商返回信息描述 · 可空 |
| `AREA_CODE` | varchar(12) | 区号 · 可空 |
| `sender_id` | varchar(24) | sender id · 可空 |

## 主键 / 索引
- 主键:`id`
- `i_msg_sent_info_ctime`:gmt_create
- `idx_msg_sent_info_msg_id`:msg_id
- `idx_msg_sent_info_sts_msg_id`:status_msg_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
