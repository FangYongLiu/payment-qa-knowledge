---
id: tbl_mns_t_channel_config_ext
object_type: Table
name: 渠道配置扩展表 (t_channel_config_ext)
aliases: [t_channel_config_ext, mns.t_channel_config_ext]
domain: infrastructure
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mns schema DDL
tags: [infrastructure, mns]
sensitivity: normal
related_services: []
---

# 渠道配置扩展表 (t_channel_config_ext)

## 用途
物理表 `mns.t_channel_config_ext`,主键 `id`。渠道配置扩展表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `ext_type` | varchar(1) | 扩展类型 |
| `ext_key` | varchar(64) | 扩展配置建 |
| `ext_value` | varchar(512) | 扩展配置值 · 可空 |
| `status` | varchar(1) | 状态 |
| `gmt_modified` | timestamp | 修改时间 |
| `gmt_create` | timestamp | 创建时间 |
| `memo` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_t_channel_config_ext_key`:ext_key

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
