---
id: tbl_assetinfo_t_asset_chain_config_param
object_type: Table
name: 资产链配置参数 (t_asset_chain_config_param)
aliases: [t_asset_chain_config_param, assetinfo.t_asset_chain_config_param]
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

# 资产链配置参数 (t_asset_chain_config_param)

## 用途
物理表 `assetinfo.t_asset_chain_config_param`,主键 `id, pkey, param_group`。资产链配置参数。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 通用指令id |
| `pkey` | varchar(50) | 键 |
| `value` | varchar(200) | 值 |
| `param_group` | varchar(50) | 组 |

## 主键 / 索引
- 主键:`id, pkey, param_group`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
