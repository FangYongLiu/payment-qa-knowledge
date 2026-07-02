---
id: tbl_ecollect_t_whitelist
object_type: Table
name: Merchant whitelist for eCollect access (t_whitelist)
aliases: [t_whitelist, ecollect.t_whitelist]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ecollect schema DDL
tags: [wallet, ecollect]
sensitivity: normal
related_services: []
---

# Merchant whitelist for eCollect access (t_whitelist)

## 用途
物理表 `ecollect.t_whitelist`,主键 `id`。Merchant whitelist for eCollect access。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(21) | PK auto-increment · 可空 |
| `mobile` | varchar(16) | Phone · 可空 |
| `uid` | varchar(8) | Botim UID (filled by cron) · 可空 |
| `allow_home` | tinyint(1) | 1=allow home, 0=deny |
| `allow_open_shop` | tinyint(1) | 1=allow open shop, 0=deny |
| `remark` | varchar(128) | Admin note · 可空 |
| `create_at` | timestamp | Create time |
| `create_by` | varchar(32) | Creator |
| `update_at` | timestamp | Update time · 可空 |
| `update_by` | varchar(32) | Updater · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_uid`:uid

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
