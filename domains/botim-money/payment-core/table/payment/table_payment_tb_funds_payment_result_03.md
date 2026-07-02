---
id: tbl_payment_tb_funds_payment_result_03
object_type: Table
name: 成功和失败才需要保存 (tb_funds_payment_result_03)
aliases: [tb_funds_payment_result_03, payment.tb_funds_payment_result_03]
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

# 成功和失败才需要保存 (tb_funds_payment_result_03)

## 用途
物理表 `payment.tb_funds_payment_result_03`,主键 `REQUEST_NO`。成功和失败才需要保存。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `PAYMENT_SEQ_NO` | varchar(32) | 成功支付流水号 |
| `PRODUCT_ORDER_NO` | varchar(64) | 产品订单号 · 可空 |
| `PAYMENT_FUNDS_ID` | decimal(18) | 机构收付信息ID，SEQ_INSTITUTION_PAYMENT_INFO · 可空 |
| `INST_PAY_NO` | varchar(64) | 提交机构订单号 · 可空 |
| `CHANNEL_PAY_NO` | varchar(64) | 渠道订单号 · 可空 |
| `FUNDS_CHANNEL_CODE` | varchar(32) | 资金通道编码 · 可空 |
| `AMOUNT` | decimal(15, 4) | 实付金额 · 可空 |
| `CURRENCY` | char(3) | 币种 · 可空 |
| `UNITY_RESULT_CODE` | varchar(32) | 统一返回码 · 可空 |
| `UNITY_RESULT_MSG` | varchar(256) | 统一返回信息 · 可空 |
| `NOTIFY_STATUS` | char | Y-已通知，N-未通知 |
| `FUNDS_RESULT_CODE` | varchar(16) | 待补 |
| `INST_PAYMENT_TIME` | timestamp | 机构支付时间 · 可空 |
| `EXTENSION` | varchar(4000) | 扩展信息 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `REQUEST_NO` | varchar(32) | 清算请求号 |
| `STATUS` | char | 状态: E 有效  U 无效 · 可空 |

## 主键 / 索引
- 主键:`REQUEST_NO`
- `IDX_FPR_GMTMODIFIED_03`:GMT_MODIFIED
- `IDX_FUNDS_PAY_RESULT_PFID_03`:PAYMENT_FUNDS_ID
- `IDX_PAYMENT_SEQ_NO_03`:PAYMENT_SEQ_NO

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
