---
id: tbl_supplier_t_supplier_info
object_type: Table
name: 供应商信息表 (t_supplier_info)
aliases: [t_supplier_info, supplier.t_supplier_info]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: supplier schema DDL
tags: [marketing, supplier]
sensitivity: normal
related_services: []
---

# 供应商信息表 (t_supplier_info)

## 用途
物理表 `supplier.t_supplier_info`,主键 `ID`。供应商信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint(32) | 待补 · 可空 |
| `Supplier_No` | varchar(64) | 供应商编号 |
| `Supplier_Name` | varchar(255) | 供应商名称 |
| `alert_balance` | decimal(15, 2) | 报警金额 |
| `settle_acct_no` | varchar(64) | 待结算账户编号 |
| `description` | varchar(1024) | 描述 · 可空 |
| `merchant_member_id` | varchar(32) | 商户会员编号 |
| `merchant_member_uid` | varchar(32) | 商户会员uid |

## 主键 / 索引
- 主键:`ID`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
