---
id: tbl_assetinfo_t_currency_pair_config
object_type: Table
name: 币对参数配置 (t_currency_pair_config)
aliases: [t_currency_pair_config, assetinfo.t_currency_pair_config]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: assetinfo schema DDL
tags: [lending, assetinfo]
sensitivity: normal
related_services: []
---

# 币对参数配置 (t_currency_pair_config)

## 用途
物理表 `assetinfo.t_currency_pair_config`,主键 `pkey, symbol`。币对参数配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `symbol` | varchar(32) | symbol |
| `pkey` | varchar(200) | 键 |
| `value` | varchar(200) | 值 |

## 主键 / 索引
- 主键:`pkey, symbol`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
