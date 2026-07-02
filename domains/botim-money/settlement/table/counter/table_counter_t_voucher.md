---
id: tbl_counter_t_voucher
object_type: Table
name: 凭证记录表 (t_voucher)
aliases: [t_voucher, counter.t_voucher]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# 凭证记录表 (t_voucher)

## 用途
物理表 `counter.t_voucher`,主键 `voucher_id`。凭证记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `voucher_id` | bigint | 凭证id |
| `voucher_date` | timestamp | 凭证记录时间 |
| `voucher_type` | tinyint(5) | 凭证类型：1-交易、2-支付  |
| `amount` | decimal(15, 2) | 金额 · 可空 |
| `unfreeze_amount` | decimal(15, 2) | 解冻金额 · 可空 |
| `currency` | varchar(5) | 币种 |
| `status` | varchar(5) | 状态  I - 初始、S -  登账成功、F - 登账失败  |
| `biz_no` | varchar(35) | 业务号 · 可空 |
| `biz_product_code` | varchar(32) | 业务产品码 · 可空 |
| `memo` | varchar(256) | 备注 · 可空 |
| `gmt_create` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`voucher_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
