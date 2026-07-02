---
id: tbl_authtoken_t_topic_config
object_type: Table
name: topic配置表 (t_topic_config)
aliases: [t_topic_config, authtoken.t_topic_config]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: authtoken schema DDL
tags: [activation, authtoken]
sensitivity: normal
related_services: []
---

# topic配置表 (t_topic_config)

## 用途
物理表 `authtoken.t_topic_config`,主键 `id`。topic配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 全局id |
| `code` | varchar(64) | code |
| `persistence` | varchar(200) | 持久化类型 · 可空 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `scanner_kyc` | varchar(20) | 扫码人需要通过kyc · 可空 |
| `delegate_decision` | varchar(20) | 能否委托决定 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
