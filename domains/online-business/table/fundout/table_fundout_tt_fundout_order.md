---
id: tbl_fundout_tt_fundout_order
object_type: Table
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (fundout schema) 2026-06-25
tags:
- fundout
- fundout
- tt_fundout_order
subdomain: fundout
module: null
sensitivity: normal
name: 出款交易订单(tt_fundout_order)
aliases:
- tt_fundout_order
related_services:
- svc_fundout
related_scenarios: []
---
# 出款交易订单(tt_fundout_order)

## 用途
出款交易订单。属 fundout 库,由 [[svc_fundout]] 读写。

## 关联关系
- **所属服务**:[[svc_fundout]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `FUNDOUT_ORDER_NO` | varchar(32) | PK / NOT NULL | 出款交易凭证号 |
| `PRODUCT_CODE` | varchar(32) | NOT NULL | 产品编码 |
| `MEMBER_ID` | varchar(32) | NOT NULL | 会员编号(该会员作为付款方参与交易) |
| `ACCOUNT_NO` | varchar(32) | NOT NULL | 储值账户 |
| `AMOUNT` | decimal(18,2) | NOT NULL | 出款金额 |
| `FEE` | decimal(18,2) | NOT NULL | 算费所得 |
| `CARD_ID` | varchar(32) |  | 认证卡号ID，会员提现时使用 |
| `CARD_NO` | varchar(32) |  | 银行卡卡号 |
| `CARD_TYPE` | char(2) |  | 借记/贷记 |
| `NAME` | varchar(256) |  | 银行卡户名 |
| `BANK_CODE` | varchar(32) |  | 银行编码 |
| `BANK_NAME` | varchar(64) |  | 银行名称 |
| `BRANCH_NAME` | varchar(256) |  | 分支行信息 |
| `BANK_LINE_NO` | char(12) |  | 联行号,如403874200010 |
| `PROV` | varchar(64) |  | 省份信息 |
| `CITY` | varchar(64) |  | 城市信息 |
| `COMPANY_PERSONAL` | char |  | 对公/对私 |
| `PURPOSE` | varchar(256) |  | 出款用途 |
| `FUNDOUT_TYPE` | varchar(10) |  | 出款类型，fundout-出款，remittance-外币汇款 |
| `QUOTATION_TOKEN` | varchar(32) |  | 报价token |
| `FUNDOUT_GRADE` | char |  | 出款时效(0:普通 1:快速 2:实时) |
| `STATUS` | varchar(16) |  | 交易状态 |
| `NOTIFY_STATUS` | char |  | 通知状态 |
| `ORDER_TIME` | timestamp |  | 下单时间 |
| `RESULT_TIME` | timestamp |  | 订单状态时间 |
| `EXTENSION` | varchar(2000) |  | 扩展信息 |
| `GMT_CREATE` | timestamp |  | 创建时间 |
| `GMT_MODIFY` | timestamp |  | 更新时间 |
| `FUNDOUT_SRC_VOUCHER_NO` | varchar(64) |  | 原始出款交易凭证号（商户订单号） |
| `PARTNER_ID` | varchar(32) |  | 平台方客户ID |
| `PARTNER_NAME` | varchar(128) |  | 平台方客户名称 |
| `MEMO` | varchar(256) |  | 备注 |
| `ACCOUNT_TYPE` | varchar(16) |  | 账户类型 |
| `FUNDOUT_BATCH_NO` | varchar(32) |  | 出款批次凭证号 |
| `FUNDOUT_SRC_BATCH_NO` | varchar(32) |  | 出款原始批次凭证号 |
| `ERROR_CODE` | varchar(16) |  | 错误编码 |
| `ERROR_MESSAGE` | varchar(256) |  | 错误描述 |
| `unity_result_code` | varchar(50) |  | 统一返回结果代码 |
| `PAY_EXPIRED_TIME` | timestamp |  | 订单支付过期时间 |
| `PAUSE_STATUS` | varchar(16) |  | 暂停状态,init,process,success |
| `BIZ_NO` | varchar(32) |  | 业务号 |
| `ACCEPTED_TIME` | timestamp |  | 订单申请成功时间 |
| `REFUNDED_TIME` | timestamp |  | 出款退票时间 |
| `currency` | char(3) |  | 货币 中国CNY 阿联酋 AED 对应java类 Currency |
| `GMT_TO_BANK_TIME` | timestamp |  | 提交至银行时间 |
| `PAYER_FEE_STRATEGY` | varchar(10) |  | 付款方费用扣取策略 |

## 主键 / 索引
- 主键:(`FUNDOUT_ORDER_NO`)
- 唯一约束:
  - `UK_FUNDOUT_QUOTATION_TOKEN` 唯一 (QUOTATION_TOKEN)
- 索引:
  - `IDX_FUNDOUT_ORDER_F_S_V_NO` (FUNDOUT_SRC_VOUCHER_NO)
  - `IDX_FUNDOUT_ORDER_GMT_CRT` (GMT_CREATE)
  - `I_FUNDOUT_BATCH_NO` (FUNDOUT_BATCH_NO)
  - `I_FUNDOUT_SRC_BATCH_NO` (FUNDOUT_SRC_BATCH_NO)
  - `TT_FUNDOUT_ORDER_GMT_MOD` (GMT_MODIFY)
  - `idx_fundout_order_pay_expiretime` (PAY_EXPIRED_TIME)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
