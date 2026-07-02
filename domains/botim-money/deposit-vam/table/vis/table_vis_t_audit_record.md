---
id: tbl_vis_t_audit_record
object_type: Table
name: 审核记录 (t_audit_record)
aliases: [t_audit_record, vis.t_audit_record]
domain: deposit-vam
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: vis schema DDL
tags: [deposit-vam, vis]
sensitivity: normal
related_services: []
---

# 审核记录 (t_audit_record)

## 用途
物理表 `vis.t_audit_record`,主键 `audit_record_id`。审核记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `audit_record_id` | bigint(11) | 审核id · 可空 |
| `bank_code` | varchar(5) | Bank Code · 可空 |
| `payment_order_no` | varchar(32) | 支付订单号 · 可空 |
| `cma_type` | varchar(4) | Cma type, CMA1/CMA2/CMA3/CMA4 · 可空 |
| `amount` | decimal(19, 4) | 金额 · 可空 |
| `currency` | char(3) | 币种 · 可空 |
| `status` | char | I-初始化，S-成功，F-失败，R-重试 |
| `operator` | varchar(32) | 操作员 · 可空 |
| `memo` | varchar(64) | memo · 可空 |
| `gmt_create` | timestamp(6) | 创建时间 · 可空 |
| `gmt_modified` | timestamp(6) | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`audit_record_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
