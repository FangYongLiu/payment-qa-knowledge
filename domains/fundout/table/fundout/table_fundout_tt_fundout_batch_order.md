---
id: tbl_fundout_tt_fundout_batch_order
object_type: Table
domain: fundout
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (fundout schema) 2026-06-25
tags:
- fundout
- fundout
- tt_fundout_batch_order
subdomain: fundout
module: null
sensitivity: normal
name: 出款批次订单表(tt_fundout_batch_order)
aliases:
- tt_fundout_batch_order
related_services:
- svc_fundout
related_scenarios: []
---
# 出款批次订单表(tt_fundout_batch_order)

## 用途
出款批次订单表。属 fundout 库,由 [[svc_fundout]] 读写。

## 关联关系
- **所属服务**:[[svc_fundout]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `FUNDOUT_BATCH_NO` | varchar(32) | PK / NOT NULL | 出款批次凭证号 |
| `FUNDOUT_SRC_BATCH_NO` | varchar(32) | NOT NULL | 出款批次原始凭证号(商户提交批次号) |
| `PRODUCT_CODE` | varchar(32) | NOT NULL | 产品编码 |
| `MEMBER_ID` | varchar(32) | NOT NULL | 该会员作为付款方参与交易 |
| `ACCOUNT_NO` | varchar(32) | NOT NULL | 储值账户 |
| `ACCOUNT_TYPE` | varchar(16) |  | 储值账户类型 |
| `TOTAL_QUANTITY` | decimal | NOT NULL | 总笔数 |
| `TOTAL_AMOUNT` | decimal(18,2) | NOT NULL | 总金额 |
| `TOTAL_FEE` | decimal(18,2) |  | 总费用 |
| `SUCCESS_QUANTITY` | decimal |  | 成功总笔数 |
| `SUCCESS_AMOUNT` | decimal(18,2) |  | 成功总金额 |
| `SUCCESS_FEE` | decimal(18,2) |  | 成功总费用 |
| `FAIL_QUANTITY` | decimal |  | 失败总笔数 |
| `FAIL_AMOUNT` | decimal(18,2) |  | 失败总金额 |
| `FAIL_FEE` | decimal(18,2) |  | 失败总费用 |
| `STATUS` | varchar(16) | NOT NULL | 批次处理状态 |
| `NOTIFY_STATUS` | char |  | 批次通知状态 |
| `FUNDOUT_GRADE` | char |  | 出款时效(0:普通 1:快速 2:实时) |
| `MEMO` | varchar(256) |  | 备注 |
| `EXTENSION` | varchar(2000) |  | 扩展信息 |
| `GMT_SUBMIT` | timestamp |  | 提交时间 |
| `GMT_CREATE` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `GMT_MODIFY` | timestamp |  | 更新时间 |
| `GMT_FINISH` | timestamp |  | 批次处理完成时间 |
| `NOTIFY_STRATEGY` | varchar(1) |  | 通知策略 1:逐笔通知 2:批量通知 0:组合通知 |
| `IDENTITY_ID` | varchar(64) |  | 会员标识 |
| `IDENTITY_TYPE` | varchar(32) |  | 标识类型 |
| `PARTNER_ID` | varchar(32) |  | 平台方ID |
| `currency` | char(3) |  | 货币 中国CNY 阿联酋 AED 对应java类 Currency |

## 主键 / 索引
- 主键:(`FUNDOUT_BATCH_NO`)
- 索引:
  - `I_BATCH_ORDER_GMT_CREATE` (GMT_CREATE)
  - `I_BATCH_ORDER_GMT_SUBMIT` (GMT_SUBMIT)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
