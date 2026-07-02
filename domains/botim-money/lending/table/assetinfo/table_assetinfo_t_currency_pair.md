---
id: tbl_assetinfo_t_currency_pair
object_type: Table
name: 币对信息 (t_currency_pair)
aliases: [t_currency_pair, assetinfo.t_currency_pair]
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

# 币对信息 (t_currency_pair)

## 用途
物理表 `assetinfo.t_currency_pair`,主键 `symbol`。币对信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `symbol` | varchar(32) | symbol |
| `base_code` | varchar(32) | baseCode · 可空 |
| `quote_code` | varchar(32) | quoteCode · 可空 |
| `name` | varchar(128) | name |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`symbol`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
