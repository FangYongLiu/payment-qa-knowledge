---
id: tbl_ups_t_ups_user_contacts
object_type: Table
name: UPS用户通讯录 (t_ups_user_contacts)
aliases: [t_ups_user_contacts, ups.t_ups_user_contacts]
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

# UPS用户通讯录 (t_ups_user_contacts)

## 用途
物理表 `ups.t_ups_user_contacts`,主键 `id`。UPS用户通讯录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `batch_id` | bigint | 批次ID |
| `member_id` | varchar(32) | 会员ID |
| `upload_pid` | varchar(32) | 上传平台ID |
| `mobile` | varchar(128) | 联系人手机号 |
| `mobile_hash` | varchar(64) | 手机号摘要 |
| `key_id` | bigint | 秘钥ID |
| `email` | varchar(32) | 联系人邮箱 · 可空 |
| `relation_id` | varchar(32) | 关联会员ID · 可空 |
| `pid` | varchar(32) | 偏好平台 payby;botim;totok; · 可空 |
| `nickname` | varchar(128) | 联系人昵称 · 可空 |
| `nickname_type` | varchar(16) | 昵称类型default; manul;： · 可空 |
| `extends` | varchar(256) | 扩展字段 · 可空 |
| `memo` | varchar(32) | 备注信息 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |
| `mobile_tag` | varchar(64) | 手机号标签 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_upc_crt`:created_time
- `inx_upc_mid`:member_id
- `inx_upc_mobilehas`:mobile_hash

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
