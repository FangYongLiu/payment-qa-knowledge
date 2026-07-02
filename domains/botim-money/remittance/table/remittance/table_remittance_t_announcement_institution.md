---
id: tbl_remittance_t_announcement_institution
object_type: Table
name: t_announcement_institution (t_announcement_institution)
aliases: [t_announcement_institution, remittance.t_announcement_institution]
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: remittance schema DDL
tags: [remittance, remittance]
sensitivity: normal
related_services: []
---

# t_announcement_institution (t_announcement_institution)

## 用途
物理表 `remittance.t_announcement_institution`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint unsigned | Primary Key · 可空 |
| `announcement_id` | bigint unsigned | Parent announcement id (t_service_announcement.id; no DB FK) |
| `institution_code` | varchar(20) | Institution (bank/wallet) code = t_bank_info.bank_code varchar(20); bank vs wallet given by parent transfer_method |
| `gmt_create` | timestamp | Creation timestamp |

## 主键 / 索引
- 主键:`id`
- `uniq_announcement_inst_code`:announcement_id, institution_code (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
