---
id: tbl_trade_t_trade_batch_order
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (trade schema) 2026-06-25
tags:
- trade
- trade
- t_trade_batch_order
subdomain: trade
module: null
sensitivity: normal
name: 交易批次订单表(t_trade_batch_order)
aliases:
- t_trade_batch_order
related_services:
- svc_tradeii
related_scenarios: []
---
# 交易批次订单表(t_trade_batch_order)

## 用途
交易批次订单表。属 trade 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `TRADE_BATCH_NO` | varchar(32) | PK / NOT NULL | 交易批次凭证号 |
| `TRADE_SRC_BATCH_NO` | varchar(64) | NOT NULL | 交易批次原始凭证号(商户提交批次号) |
| `BIZ_PRODUCT_CODE` | varchar(16) | NOT NULL | 业务产品编码 |
| `TRADE_TYPE` | varchar(16) | NOT NULL | 交易类型 |
| `MEMBER_ID` | varchar(32) | NOT NULL | 该会员作为付款方参与交易 |
| `ACCOUNT_NO` | varchar(32) | NOT NULL | 储值账户 |
| `ACCOUNT_TYPE` | varchar(16) | NOT NULL | 储值账户类型 |
| `PARTNER_ID` | varchar(32) | NOT NULL | 平台方客户编号 |
| `PARTNER_NAME` | varchar(128) |  | 平台方客户名称 |
| `TOTAL_QUANTITY` | decimal | NOT NULL | 总笔数 |
| `TOTAL_AMOUNT` | decimal(15,4) | NOT NULL | 总金额 |
| `TOTAL_FEE` | decimal(15,4) |  | 总费用 |
| `SUCCESS_QUANTITY` | decimal |  | 成功总笔数 |
| `SUCCESS_AMOUNT` | decimal(15,4) |  | 成功总金额 |
| `SUCCESS_FEE` | decimal(15,4) |  | 成功总费用 |
| `FAIL_QUANTITY` | decimal |  | 失败总笔数 |
| `FAIL_AMOUNT` | decimal(15,4) |  | 失败总金额 |
| `FAIL_FEE` | decimal(15,4) |  | 失败总费用 |
| `STATUS` | varchar(16) | NOT NULL | 批次处理状态 |
| `IS_NOTIFIED` | char |  | 是否通知成功 |
| `MEMO` | varchar(256) |  | 备注 |
| `EXTENSION` | varchar(2000) |  | 扩展信息 |
| `GMT_SUBMIT` | timestamp |  | 提交时间 |
| `GMT_CREATE` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 更新时间 |
| `NOTIFY_STRATEGY` | varchar(8) |  | 通知策略,SG-单笔通知,BA-批量通知,BO-单笔批量都通知 |
| `CURRENCY` | char(3) |  | 币种 |

## 主键 / 索引
- 主键:(`TRADE_BATCH_NO`)
- 索引:
  - `I_TRADE_BATCH_ORDER_GMT_CREATE` (GMT_CREATE)
  - `I_TRADE_BATCH_ORDER_GMT_SUBMIT` (GMT_SUBMIT)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
