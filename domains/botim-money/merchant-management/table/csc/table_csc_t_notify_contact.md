---
id: tbl_csc_t_notify_contact
object_type: Table
name: 通知联系人 (t_notify_contact)
aliases: [t_notify_contact, csc.t_notify_contact]
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

# 通知联系人 (t_notify_contact)

## 用途
物理表 `csc.t_notify_contact`,主键 `contact_id`。通知联系人。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `contact_id` | bigint | 联系人ID · 可空 |
| `contact_name` | varchar(128) | 联系人名称 |
| `email` | varchar(255) | 邮箱地址 |
| `mobile` | varchar(128) | 手机号 · 可空 |
| `totok_id` | varchar(128) | TotokID · 可空 |
| `botim_id` | varchar(128) | BotimId · 可空 |
| `normal_notify_type` | varchar(10) | 普通通知类型：EMAIL,SMS,TOTOK |
| `urgent_notify_type` | varchar(10) | 紧急通知类型：EMAIL,SMS,TOTOK |
| `enable_flag` | char | 启用标识：Y=启用，N=停用 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`contact_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
