---
id: tbl_payment_tb_payment_service_code
object_type: Table
name: tb_payment_service_code (tb_payment_service_code)
aliases: [tb_payment_service_code, payment.tb_payment_service_code]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: payment schema DDL
tags: [payment-core, payment]
sensitivity: normal
related_services: []
---

# tb_payment_service_code (tb_payment_service_code)

## 用途
物理表 `payment.tb_payment_service_code`,主键 `CODE`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CODE` | varchar(32) | 代码 |
| `DESCRITION` | varchar(64) | 描述 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`CODE`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
