---
id: tbl_reconciliation_t_channel_http_config
object_type: Table
name: 渠道http配置 (t_channel_http_config)
aliases: [t_channel_http_config, reconciliation.t_channel_http_config]
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

# 渠道http配置 (t_channel_http_config)

## 用途
物理表 `reconciliation.t_channel_http_config`,主键 `config_id`。渠道http配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `config_id` | bigint(17) | 主键 配置ID |
| `fund_channel_code` | varchar(32) | 渠道编号 · 可空 |
| `biz_type` | varchar(4) | 业务类型 · 可空 |
| `status` | varchar(8) | 状态 Y:生效 N:失效 · 可空 |
| `url` | varchar(255) | 请求地址,用于请求对账单地址 · 可空 |
| `http_type` | varchar(8) | 请求方式 Get Post · 可空 |
| `params` | varchar(512) | 参数 参数以map形式存储  · 可空 |
| `file_name_rule` | varchar(512) | 文件名称规则,下载到本地保存规则 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `operator` | varchar(64) | 创建者 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`config_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
