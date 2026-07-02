---
id: tbl_custom_t_iap_config
object_type: Table
name: iap商户和配置关联表 (t_iap_config)
aliases: [t_iap_config, custom.t_iap_config]
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

# iap商户和配置关联表 (t_iap_config)

## 用途
物理表 `custom.t_iap_config`,主键 `id`。iap商户和配置关联表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(17) | 主键 |
| `title` | varchar(64) | 标题，用于展示在App上选择的标题 |
| `config_name` | varchar(64) | 配置名称 |
| `config_desc` | varchar(512) | 配置描述 |
| `host_app` | varchar(16) | 载体 |
| `version` | varchar(32) | 最小支持版本 |
| `host_package` | varchar(32) | 载体包名 · 可空 |
| `logo_icon` | varchar(255) | 载体包名 · 可空 |
| `update_flag` | char | 更新标记 · 可空 |
| `redirect_url` | varchar(255) | 重定向路由地址 |
| `download_url` | varchar(255) | app下载地址 · 可空 |
| `biz_type` | varchar(16) | iap业务类型 |
| `status` | char | 状态 Y:启用 N:停用 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 创建时间 |
| `ios_host_package` | varchar(32) | ios主体包名 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
