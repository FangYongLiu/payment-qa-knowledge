---
id: tbl_marketorder_t_order_detail
object_type: Table
name: 订单明细表 (t_order_detail)
aliases: [t_order_detail, marketorder.t_order_detail]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketorder schema DDL
tags: [marketing, marketorder]
sensitivity: normal
related_services: []
---

# 订单明细表 (t_order_detail)

## 用途
物理表 `marketorder.t_order_detail`,主键 `id`。订单明细表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `order_no` | bigint(18) | 订单编号 |
| `phone_number` | varchar(16) | 电话号码 · 可空 |
| `bill_id` | bigint(18) | 账单号 · 可空 |
| `account_id` | bigint(18) | 账户id · 可空 |
| `package_type` | varchar(20) | 套餐类型 · 可空 |
| `service_provider` | varchar(20) | 服务商 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `gmt_created` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`id`
- `uk_order_no`:order_no (UNIQUE)
- `idx_bill_id`:bill_id

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
