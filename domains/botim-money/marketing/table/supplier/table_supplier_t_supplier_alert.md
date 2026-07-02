---
id: tbl_supplier_t_supplier_alert
object_type: Table
name: 供应商告警表 (t_supplier_alert)
aliases: [t_supplier_alert, supplier.t_supplier_alert]
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

# 供应商告警表 (t_supplier_alert)

## 用途
物理表 `supplier.t_supplier_alert`,主键 `id`。供应商告警表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 |
| `alert_info` | varchar(150) | 告警信息 · 可空 |
| `alert_type` | varchar(32) | 告警类型（SUPPLIER_BALANCE：供应商余额告警;ORDER_COM_AMT_CHECK:订单佣金金额核对告警） · 可空 |
| `supplier_no` | varchar(32) | 供应商no · 可空 |
| `status` | varchar(16) | 告警状态：NORMAL正常,ERROR有错误 |
| `gmt_created` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `extension` | varchar(10000) | 拓展信息 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
