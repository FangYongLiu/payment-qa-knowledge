---
id: tbl_casheatm_t_store_function
object_type: Table
name: t_store_function (t_store_function)
aliases: [t_store_function, casheatm.t_store_function]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: casheatm schema DDL
tags: [online-business, casheatm]
sensitivity: normal
related_services: []
---

# t_store_function (t_store_function)

## 用途
物理表 `casheatm.t_store_function`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `store_id` | bigint | 店铺id |
| `function_type` | varchar(32) | 功能类型 |
| `ceil_currency_code` | varchar(50) | 待补 · 可空 |
| `ceil_amount` | decimal(19, 4) | 上限 · 可空 |
| `floor_currency_code` | varchar(50) | 待补 · 可空 |
| `floor_amount` | decimal(19, 4) | 下线 · 可空 |
| `status` | varchar(32) | 收单状态 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `i_sf_sf`:store_id, function_type (UNIQUE)
- `i_sf_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
