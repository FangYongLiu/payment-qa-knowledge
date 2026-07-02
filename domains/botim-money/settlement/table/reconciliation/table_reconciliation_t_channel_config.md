---
id: tbl_reconciliation_t_channel_config
object_type: Table
name: 渠道参数配置 (t_channel_config)
aliases: [t_channel_config, reconciliation.t_channel_config]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 渠道参数配置 (t_channel_config)

## 用途
物理表 `reconciliation.t_channel_config`,主键 `id`。渠道参数配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `param_key` | varchar(32) | 参数key · 可空 |
| `param_value` | varchar(256) | 参数值 · 可空 |
| `status` | varchar(4) | 状态,是否启用 Y:Yes  N:No · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `index_fundChannelKey`:fund_channel_code, param_key (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
