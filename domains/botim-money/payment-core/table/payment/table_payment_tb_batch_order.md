---
id: tbl_payment_tb_batch_order
object_type: Table
name: tb_batch_order (tb_batch_order)
aliases: [tb_batch_order, payment.tb_batch_order]
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

# tb_batch_order (tb_batch_order)

## 用途
物理表 `payment.tb_batch_order`,主键 `BATCH_SEQ_NO`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `BATCH_SEQ_NO` | decimal(16) | 批次流水号:系统唯一 |
| `BATCH_NO` | varchar(32) | 批次订单号 |
| `BATCH_TYPE` | char | 批次类型 |
| `MACHINE_NAME` | varchar(32) | 机器域名 · 可空 |
| `PRODUCT_CODE` | varchar(32) | 产品编码 · 可空 |
| `PROCESS_SEQ_NO` | varchar(32) | 冻结扣款=冻结流水号, 扣款=支付订单号 · 可空 |
| `MEMBER_ID` | varchar(32) | 会员ID |
| `ACCOUNT_NO` | varchar(32) | 储值账户 |
| `PAYABLE_AMOUNT` | decimal(16, 4) | 应付金额 |
| `PAYER_FEE` | decimal(16, 4) | 应付费用 |
| `CURRENCY` | char(3) | 币种 · 可空 |
| `STORE_KEY` | varchar(256) | 分布式存储文件名 · 可空 |
| `TOTAL_NUM` | decimal(16) | 总笔数 |
| `END_NUM` | decimal(16) | 已处理笔数 |
| `CALLBACK_ADDR` | varchar(256) | 回调地址 |
| `STATUS` | char | 批次处理状态 |
| `MEMO` | varchar(256) | 备注信息 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 最后修改时间 |

## 主键 / 索引
- 主键:`BATCH_SEQ_NO`
- `IDX_BATCH_ORDER_GMTMODIFY`:GMT_MODIFY
- `IDX_BO_BN`:BATCH_NO

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
