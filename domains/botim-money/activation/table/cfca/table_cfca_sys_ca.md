---
id: tbl_cfca_sys_ca
object_type: Table
name: sys_ca (sys_ca)
aliases: [sys_ca, cfca.sys_ca]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cfca schema DDL
tags: [activation, cfca]
sensitivity: normal
related_services: []
---

# sys_ca (sys_ca)

## 用途
物理表 `cfca.sys_ca`,主键 `caid`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `caid` | bigint(10) | 待补 · 可空 |
| `ca_name` | varchar(255) | 待补 · 可空 |
| `cert_chain` | longblob | 待补 · 可空 |
| `cert_dn` | varchar(255) | 待补 · 可空 |
| `cert_entity` | longblob | 待补 · 可空 |
| `cert_sn` | varchar(255) | 待补 |
| `issuerdn` | varchar(255) | 待补 · 可空 |
| `not_after` | datetime | 待补 · 可空 |
| `not_before` | datetime | 待补 · 可空 |
| `sign_alg` | varchar(255) | 待补 · 可空 |
| `type` | bigint(11) | 待补 · 可空 |

## 主键 / 索引
- 主键:`caid`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
