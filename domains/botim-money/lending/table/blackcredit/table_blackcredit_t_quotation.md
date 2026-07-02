---
id: tbl_blackcredit_t_quotation
object_type: Table
name: 汇率报价 (t_quotation)
aliases: [t_quotation, blackcredit.t_quotation]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: blackcredit schema DDL
tags: [lending, blackcredit]
sensitivity: normal
related_services: []
---

# 汇率报价 (t_quotation)

## 用途
物理表 `blackcredit.t_quotation`,主键 `foreign_code, local_code`。汇率报价。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `foreign_code` | varchar(8) | 币对代码 |
| `local_code` | varchar(8) | 币对代码 |
| `sell_rate` | decimal(10, 6) | 卖汇率 |
| `buy_rate` | decimal(10, 6) | 买汇率 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`foreign_code, local_code`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
