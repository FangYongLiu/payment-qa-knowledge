---
id: tbl_collection_t_col_push_config
object_type: Table
name: t_col_push_config (t_col_push_config)
aliases: [t_col_push_config, collection.t_col_push_config]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# t_col_push_config (t_col_push_config)

## 用途
物理表 `collection.t_col_push_config`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(11) | 主健 · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `update_by` | varchar(100) | 更新人员 · 可空 |
| `uid` | varchar(50) | 唯一id |
| `start` | smallint(5) | 逾期开始天数 · 可空 |
| `end` | smallint(5) | 逾期结束天数 · 可空 |
| `time` | varchar(100) | 启动时间逗号分隔 · 可空 |
| `title` | varchar(50) | 标题 |
| `join_id` | varchar(50) | 外部id · 可空 |
| `content` | varchar(500) | 内容 · 可空 |
| `remarks` | varchar(500) | 备注 · 可空 |
| `param` | varchar(50) | 参数 · 可空 |
| `target` | tinyint(5) | 目标0本人 1紧急联系人 · 可空 |
| `partner_id` | varchar(50) | 平台 · 可空 |
| `send_type` | tinyint(5) | 1 模版 2推送 · 可空 |
| `type` | tinyint(5) | 类型 1电话 2totok 3whatsapp 4短信 |
| `enabled` | tinyint(5) | 状态 |
| `product` | tinyint(5) | 产品 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
