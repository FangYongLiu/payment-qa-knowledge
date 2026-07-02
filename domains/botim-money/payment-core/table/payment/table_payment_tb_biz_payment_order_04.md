---
id: tbl_payment_tb_biz_payment_order_04
object_type: Table
name: 业务支付订单 (tb_biz_payment_order_04)
aliases: [tb_biz_payment_order_04, payment.tb_biz_payment_order_04]
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

# 业务支付订单 (tb_biz_payment_order_04)

## 用途
物理表 `payment.tb_biz_payment_order_04`,主键 `BIZ_PAYMENT_SEQ_NO`。业务支付订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `BIZ_PAYMENT_SEQ_NO` | varchar(32) | 业务支付订单流水号 |
| `ORIG_VOUCHER_NO` | varchar(64) | 原始凭证号 |
| `PRODUCT_CODE` | varchar(32) | 产品系统标识 |
| `PAYMENT_CODE` | varchar(32) | 支付编码 |
| `PAYMENT_ORDER_NO` | varchar(64) | 支付订单号，收单服务支付订单流水号 |
| `BIZ_PAYMENT_TYPE` | varchar(10) | 业务支付类型 |
| `RELATE_BIZ_PAYMENT_SEQ_NO` | varchar(32) | 相关支付订单流水号 · 可空 |
| `BIZ_PAYMENT_STATE` | char | 待补 |
| `CALLBACK_ADDR` | varchar(200) | 回调地址 · 可空 |
| `CLIENT_ID` | varchar(10) | 客户端系统编号 |
| `EXTENSION` | varchar(1000) | 扩展信息，鉴权token：_AuthToken_ · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `BIZ_SUB_STATE` | varchar(16) | 业务支付订单子状态 · 可空 |
| `CONTROL_PARAM` | varchar(128) | 控制参数，半角逗号分隔，自动结算：AUTO_SETTLE，自动分账：AUTO_SPLIT，CREDIT_SETTLE：授信结算，BAD_DEBIT_SETTLE：坏账结算 · 可空 |
| `PAUSE_FLAG` | char | 暂停标识，风控暂停：R，支付暂停：P，非暂停：空 · 可空 |
| `DUPLICATE_FLAG` | char | 重复标识，重复：Y，非重复：空 · 可空 |
| `PRODUCT_ORDER_NO` | varchar(32) | 产品订单号 · 可空 |
| `GEN_GROUP_CODE` | varchar(32) | 生成集编码 · 可空 |
| `CUR_PAYMENT_SEQ_NO` | varchar(32) | 当前支付流水号 · 可空 |
| `BIZ_PRODUCT_CODE` | varchar(32) | 业务产品编码 · 可空 |
| `SAVING_POT_STATUS` | varchar(10) | 存钱罐申购或赎回的状态，PI-申购初始，PP-申购处理中，PS-申购成功，PF-申购失败，RI-赎回初始，RP-赎回处理中，RS-赎回成功，RF-赎回失败 · 可空 |

## 主键 / 索引
- 主键:`BIZ_PAYMENT_SEQ_NO`
- `UIDX_PAYMENT_KEY_04`:PAYMENT_ORDER_NO, PRODUCT_CODE (UNIQUE)
- `IDX_BPO_GMTMODIFIED_04`:GMT_MODIFIED
- `I_BIZ_PAYMENT_ORDER_RBPSN_04`:RELATE_BIZ_PAYMENT_SEQ_NO

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
