---
id: tbl_payment_tb_product_account_config
object_type: Table
name: 业务产品码与账户关系配置表 (tb_product_account_config)
aliases: [tb_product_account_config, payment.tb_product_account_config]
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

# 业务产品码与账户关系配置表 (tb_product_account_config)

## 用途
物理表 `payment.tb_product_account_config`,主键 `ID`。业务产品码与账户关系配置表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | int | 主键 · 可空 |
| `BIZ_PRODUCT_CODE` | varchar(32) | 业务产品码 |
| `PARTY_ROLE` | varchar(32) | 参与方角色 |
| `FROM_ROLE` | varchar(32) | 来源角色 · 可空 |
| `ACCOUNT_TYPE` | varchar(32) | 账户类型 · 可空 |
| `DEFAULT_ACCOUNT` | varchar(32) | 默认账户 · 可空 |
| `currency` | char(3) | 币种 · 可空 |
| `REQUIRED` | char | 必填标志：Y-必须；N-非必须 |
| `AUTO_OPEN` | char | 是否自动开户：Y-是；N-否 |
| `STATUS` | char | 状态：1-有效；0-无效 |
| `GMT_CREATE` | timestamp | 创建时间 · 可空 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`ID`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
