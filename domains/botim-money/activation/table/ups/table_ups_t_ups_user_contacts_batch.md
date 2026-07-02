---
id: tbl_ups_t_ups_user_contacts_batch
object_type: Table
name: UPS用户通讯录上传订单表 (t_ups_user_contacts_batch)
aliases: [t_ups_user_contacts_batch, ups.t_ups_user_contacts_batch]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ups schema DDL
tags: [activation, ups]
sensitivity: normal
related_services: []
---

# UPS用户通讯录上传订单表 (t_ups_user_contacts_batch)

## 用途
物理表 `ups.t_ups_user_contacts_batch`,主键 `id`。UPS用户通讯录上传订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `upload_pid` | varchar(32) | 上传平台ID |
| `member_id` | varchar(32) | 会员ID |
| `upload_content` | varchar(32) | 上传内容 |
| `status` | varchar(16) | 订单状态 |
| `created_time` | timestamp | 创建时间 |
| `udpated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `idx_created_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
