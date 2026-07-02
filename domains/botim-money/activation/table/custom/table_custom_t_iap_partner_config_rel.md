---
id: tbl_custom_t_iap_partner_config_rel
object_type: Table
name: iap商户和配置关联表 (t_iap_partner_config_rel)
aliases: [t_iap_partner_config_rel, custom.t_iap_partner_config_rel]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: custom schema DDL
tags: [activation, custom]
sensitivity: normal
related_services: []
---

# iap商户和配置关联表 (t_iap_partner_config_rel)

## 用途
物理表 `custom.t_iap_partner_config_rel`,主键 `id`。iap商户和配置关联表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 主键 |
| `iap_partner_id` | bigint(17) | iap商户表ID |
| `iap_config_id` | bigint(17) | iap业务类型 |
| `is_recommend` | char | 是否推荐 |
| `sort_index` | int | 顺序 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
