---
id: tbl_cfca_log_conf
object_type: Table
name: log_conf (log_conf)
aliases: [log_conf, cfca.log_conf]
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

# log_conf (log_conf)

## 用途
物理表 `cfca.log_conf`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | 待补 · 可空 |
| `authreqfail` | bigint(1) | 待补 · 可空 |
| `authreqsuc` | bigint(1) | 待补 · 可空 |
| `authresponsefail` | bigint(1) | 待补 · 可空 |
| `authresponsesuc` | bigint(1) | 待补 · 可空 |
| `dereglistfail` | bigint(1) | 待补 · 可空 |
| `dereglistsuc` | bigint(1) | 待补 · 可空 |
| `deregreqfail` | bigint(1) | 待补 · 可空 |
| `deregreqsuc` | bigint(1) | 待补 · 可空 |
| `regreqfail` | bigint(1) | 待补 · 可空 |
| `regreqsuc` | bigint(1) | 待补 · 可空 |
| `regresponsefail` | bigint(1) | 待补 · 可空 |
| `regresponsesuc` | bigint(1) | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
