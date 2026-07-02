---
id: tbl_supplier_t_supplier_channel_regulation
object_type: Table
name: 供应商渠道信息规则表 (t_supplier_channel_regulation)
aliases: [t_supplier_channel_regulation, supplier.t_supplier_channel_regulation]
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

# 供应商渠道信息规则表 (t_supplier_channel_regulation)

## 用途
物理表 `supplier.t_supplier_channel_regulation`,主键 `id`。供应商渠道信息规则表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(16) | 待补 · 可空 |
| `Supplier_No` | varchar(64) | 供应商编号 |
| `SUPPLIER_CHANNEL_CODE` | varchar(32) | 渠道编号 |
| `PROVIDER_CODE` | varchar(32) | 供应商编号 |
| `PRODUCT_CODE` | varchar(32) | 产品编号 |
| `STATUS` | varchar(16) | 是否可用：VALID（可用），INVALID（不可用） |
| `API_ID` | varchar(32) | IOID |
| `API_TYPE` | varchar(8) | apiType：Input ; Output |
| `Operation_TYPE` | varchar(16) | Operation:Inquiry;Payment;Both |
| `regulation_name` | varchar(255) | supplier定义的规则名字 · 可空 |
| `name` | varchar(255) | 渠道api字段的名字 |
| `Description` | varchar(512) | api的描述 · 可空 |
| `Min_Length` | varchar(8) | 最小长度 |
| `Max_Length` | varchar(8) | 最大长度 |
| `Valid_Lengths` | varchar(16) | 有效长度 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 · 可空 |
| `MEMO` | varchar(255) | 备注 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
