---
id: tbl_pbsdb_tb_trade_info
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (pbsdb schema) 2026-06-25
tags:
- pbsdb
- pricing
- tb_trade_info
subdomain: pricing
module: null
sensitivity: normal
name: 交易记录表(tb_trade_info)
aliases:
- tb_trade_info
related_services:
- svc_pbs
related_scenarios: []
---
# 交易记录表(tb_trade_info)

## 用途
交易记录表。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `TRADE_INFO_ID` | decimal(18) | PK / NOT NULL | 消费记录ID |
| `BIZ_PRODUCT_CODE` | varchar(20) |  | 业务产品码 |
| `REQUEST_NO` | varchar(32) |  | 请求号 |
| `CLIENT_ID` | varchar(20) |  | 平台的系统名称 |
| `TRADE_COUNT` | decimal(12) |  | 消费次数 |
| `MEMBER_ID` | varchar(32) |  | 商户号 |
| `PARTNER_ID` | varchar(32) |  | 平台方 |
| `STATUS` | varchar(10) |  | 1未算费,2算费成功,3算费失败 |
| `FEE_AMOUNT` | decimal(15,2) |  | 手续费 |
| `EXTENTION` | varchar(200) |  | 扩展参数 |
| `CUMULATIVE_FLOW` | decimal(12) |  | 累计流量 |
| `BILL_NO` | decimal(18) |  | 账单号 |
| `GMT_CREATE` | timestamp |  | 创建时间 |
| `GMT_MODIFIED` | timestamp |  | 修改时间 |
| `GMT_TRANSACTION` | timestamp |  | 消费时间 |

## 主键 / 索引
- 主键:(`TRADE_INFO_ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
