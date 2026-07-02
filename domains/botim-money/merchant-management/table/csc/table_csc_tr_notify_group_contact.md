---
id: tbl_csc_tr_notify_group_contact
object_type: Table
name: 通知组联系人关联 (tr_notify_group_contact)
aliases: [tr_notify_group_contact, csc.tr_notify_group_contact]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: csc schema DDL
tags: [merchant-management, csc]
sensitivity: normal
related_services: []
---

# 通知组联系人关联 (tr_notify_group_contact)

## 用途
物理表 `csc.tr_notify_group_contact`,主键 `relate_id`。通知组联系人关联。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `relate_id` | bigint | 关联ID · 可空 |
| `group_id` | bigint | 组ID |
| `contact_id` | bigint | 联系人ID |
| `create_time` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`relate_id`
- `uk_group_id_contact_id`:group_id, contact_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
