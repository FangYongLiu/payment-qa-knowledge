---
id: tbl_payment_tb_biz_config_04
object_type: Table
name: 业务支付配置，量级同TB_PAYMENT_ORDER (tb_biz_config_04)
aliases: [tb_biz_config_04, payment.tb_biz_config_04]
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

# 业务支付配置，量级同TB_PAYMENT_ORDER (tb_biz_config_04)

## 用途
物理表 `payment.tb_biz_config_04`,主键 `CONFIG_ID`。业务支付配置，量级同TB_PAYMENT_ORDER。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CONFIG_ID` | decimal(18) | 配置Id |
| `BIZ_PAYMENT_SEQ_NO` | varchar(32) | 业务支付号 |
| `GEN_CODE` | varchar(32) | 生成编码 |
| `PAYMENT_SEQ_NO` | varchar(32) | 支付流水号 |
| `PRE_GEN_CODE` | varchar(32) | 上一步生成编码 · 可空 |
| `NEXT_GEN_CODE` | varchar(32) | 下一步生成编码 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |
| `RETRY_TIMES` | decimal(8) | 重试次数 · 可空 |
| `PAYMENT_SUB_STATE` | varchar(16) | 支付子状态 · 可空 |
| `PRIORITY` | decimal(6) | 支付优先级 · 可空 |
| `AUTO_SETTLE` | char | Y=自动结算，N=外部结算 · 可空 |

## 主键 / 索引
- 主键:`CONFIG_ID`
- `IDX_BIZ_CONFIG_GMT_MOD_04`:GMT_MODIFY

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
