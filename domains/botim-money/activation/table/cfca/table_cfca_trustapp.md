---
id: tbl_cfca_trustapp
object_type: Table
name: trustapp (trustapp)
aliases: [trustapp, cfca.trustapp]
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

# trustapp (trustapp)

## 用途
物理表 `cfca.trustapp`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(10) | 待补 · 可空 |
| `appid` | bigint(11) | 待补 |
| `appid_info` | varchar(255) | 待补 · 可空 |
| `appname` | varchar(255) | 待补 · 可空 |
| `info` | varchar(4000) | 待补 |
| `branch_code` | varchar(50) | 待补 · 可空 |
| `ca_name` | varchar(20) | 待补 · 可空 |
| `remark` | varchar(255) | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- `IDX_TRUSTAPP_TRUST_ID`:appid (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
