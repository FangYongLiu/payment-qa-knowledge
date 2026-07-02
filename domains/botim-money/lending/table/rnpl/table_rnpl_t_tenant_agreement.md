---
id: tbl_rnpl_t_tenant_agreement
object_type: Table
name: t_tenant_agreement (t_tenant_agreement)
aliases: [t_tenant_agreement, rnpl.t_tenant_agreement]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rnpl schema DDL
tags: [lending, rnpl]
sensitivity: normal
related_services: []
---

# t_tenant_agreement (t_tenant_agreement)

## 用途
物理表 `rnpl.t_tenant_agreement`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(10) | 待补 · 可空 |
| `user_id` | varchar(32) | user_id |
| `rent_contract_no` | varchar(64) | rent_contract_no |
| `signed_time` | timestamp | signed_time |
| `agreement_type` | varchar(32) | agreement_type |
| `file_tag` | varchar(128) | file_tag · 可空 |
| `create_time` | timestamp | 待补 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `ix_ct`:create_time
- `ix_order_no`:rent_contract_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
