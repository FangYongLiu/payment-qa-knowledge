---
id: tbl_payment_tb_payment_service
object_type: Table
name: 支付服务配置 (tb_payment_service)
aliases: [tb_payment_service, payment.tb_payment_service]
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

# 支付服务配置 (tb_payment_service)

## 用途
物理表 `payment.tb_payment_service`,主键 `PS_ID`。支付服务配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `PS_ID` | bigint | 流程配置ID · 可空 |
| `PS_CODE` | varchar(16) | 支付服务编码 |
| `DESCRITION` | varchar(64) | 描述 |
| `PAYMENT_CODE` | varchar(16) | 产品编码 |
| `PAYMENT_TYPE` | varchar(10) | I-入款,O-出款,T-转账,R-退款到卡,F-退票,B-退款到账户 |
| `PROCESS_FLAG` | char | 待补 |
| `GMT_EFFECT` | timestamp | 生效时间 |
| `GMT_EXPIRED` | timestamp | 失效时间，空则代表永不失效 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |
| `PS_GROUP` | varchar(128) | 属于当前支付服务分组的子支付服务，已逗号分隔，执行时将根据列出的顺序执行，并在作为一个清算请求，例如205,305 · 可空 |

## 主键 / 索引
- 主键:`PS_ID`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
