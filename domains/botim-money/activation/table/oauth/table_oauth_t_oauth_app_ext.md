---
id: tbl_oauth_t_oauth_app_ext
object_type: Table
name: 三方应用扩展 (t_oauth_app_ext)
aliases: [t_oauth_app_ext, oauth.t_oauth_app_ext]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: oauth schema DDL
tags: [activation, oauth]
sensitivity: normal
related_services: []
---

# 三方应用扩展 (t_oauth_app_ext)

## 用途
物理表 `oauth.t_oauth_app_ext`,主键 `id`。三方应用扩展。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识 |
| `app_id` | bigint | 依赖t_oauth_client_app.id |
| `app_name` | varchar(64) | 第三方应用名称。冗余。 |
| `client_id` | varchar(64) | 第三方应用编号。冗余。 |
| `classify` | varchar(64) | 扩展分类 |
| `bond` | varchar(128) | 扩展键 |
| `val` | varchar(1000) | 扩展值 |
| `ext_name` | varchar(32) | 扩展名称 |
| `use_status` | varchar(64) | 状态：active | inactive |
| `ordinal` | varchar(64) | 排序 |
| `create_time` | varchar(64) | 创建时间 |
| `update_time` | varchar(64) | 更新时间 |
| `enable_flag` | varchar(2) | 可用标志。Y可用，或者其它代表“删除” |

## 主键 / 索引
- 主键:`id`
- `idx_toae_appid`:app_id
- `idx_toae_classify`:classify

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
