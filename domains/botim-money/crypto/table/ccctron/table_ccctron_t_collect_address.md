---
id: tbl_ccctron_t_collect_address
object_type: Table
name: 归集地址(分区) (t_collect_address)
aliases: [t_collect_address, ccctron.t_collect_address]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccctron schema DDL
tags: [crypto, ccctron]
sensitivity: normal
related_services: []
---

# 归集地址(分区) (t_collect_address)

## 用途
物理表 `ccctron.t_collect_address`,主键 `id`。归集地址(分区)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id(yyyyMMdd999999999) |
| `batch_id` | bigint | 批次id |
| `address` | varchar(200) | 地址 |
| `fail_collect_crny_count` | int | 失败归集资产个数 · 可空 |
| `success_collect_crny_count` | int | 成功归集资产个数 · 可空 |
| `total_collect_crny_count` | int | 总共归集资产个数 · 可空 |
| `fuel_amount` | decimal(23, 8) | 加油金额 · 可空 |
| `fuel_order_id` | bigint | 加油转账订单 · 可空 |
| `status` | varchar(50) | 订单状态 |
| `success` | varchar(50) | 是否成功 · 可空 |
| `fail_code` | varchar(50) | 失败代码 · 可空 |
| `fail_message` | varchar(200) | 失败消息 · 可空 |
| `data_version` | bigint | 数据版本 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `fuel_cent` | decimal(32) | 加油(分) · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_ca_addr`:batch_id, address (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
