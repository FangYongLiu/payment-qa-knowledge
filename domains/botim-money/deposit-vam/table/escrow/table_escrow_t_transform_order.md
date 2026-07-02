---
id: tbl_escrow_t_transform_order
object_type: Table
name: 转换订单 (t_transform_order)
aliases: [t_transform_order, escrow.t_transform_order]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: escrow schema DDL
tags: [deposit-vam, escrow]
sensitivity: normal
related_services: []
---

# 转换订单 (t_transform_order)

## 用途
物理表 `escrow.t_transform_order`,主键 `order_id`。转换订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `order_id` | bigint(32) | 订单id · 可空 |
| `order_no` | varchar(32) | 订单号 |
| `member_id` | varchar(16) | 会员id · 可空 |
| `amount` | decimal(16, 2) | 金额 |
| `currency` | char(3) | 币种 · 可空 |
| `trans_status` | char | 交易状态,S-成功,I-处理中 · 可空 |
| `trans_time` | timestamp | 交易时间 · 可空 |
| `trans_type` | varchar(10) | 交易类型,split-拆单 · 可空 |
| `biz_product_code` | varchar(6) | 业务产品码 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `memo` | varchar(64) | 备注 · 可空 |

## 主键 / 索引
- 主键:`order_id`
- `uk_transform_order_no`:order_no (UNIQUE)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
