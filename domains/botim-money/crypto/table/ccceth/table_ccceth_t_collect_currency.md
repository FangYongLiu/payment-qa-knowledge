---
id: tbl_ccceth_t_collect_currency
object_type: Table
name: 归集资产(分区) (t_collect_currency)
aliases: [t_collect_currency, ccceth.t_collect_currency]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccceth schema DDL
tags: [crypto, ccceth]
sensitivity: normal
related_services: []
---

# 归集资产(分区) (t_collect_currency)

## 用途
物理表 `ccceth.t_collect_currency`,主键 `id`。归集资产(分区)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id(yyyyMMdd999999999) |
| `address_id` | bigint | 批次id |
| `currency_code` | varchar(50) | 资产代码 |
| `status` | varchar(200) | 订单状态 |
| `collect_order_id` | bigint | 归集转账订单 · 可空 |
| `data_version` | bigint | 数据版本 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_cat_ast`:address_id, currency_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
