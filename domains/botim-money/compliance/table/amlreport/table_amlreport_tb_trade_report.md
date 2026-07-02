---
id: tbl_amlreport_tb_trade_report
object_type: Table
name: 交易统计 (tb_trade_report)
aliases: [tb_trade_report, amlreport.tb_trade_report]
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: amlreport schema DDL
tags: [compliance, amlreport]
sensitivity: normal
related_services: []
---

# 交易统计 (tb_trade_report)

## 用途
物理表 `amlreport.tb_trade_report`,主键 `id`。交易统计。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `member_id` | varchar(32) | 会员ID · 可空 |
| `report_date` | int | 统计日期 yyyyMMdd · 可空 |
| `recharges_cnt` | int | 充值尝试总次数 · 可空 |
| `recharges_s_cnt` | int | 充值成功次数 · 可空 |
| `recharges_amt` | decimal(15, 4) | 充值尝试总金额 · 可空 |
| `recharges_s_amt` | decimal(15, 4) | 充值成功金额 · 可空 |
| `recharges_max` | decimal(15, 4) | 充值尝试最大金额 · 可空 |
| `recharges_s_max` | decimal(15, 4) | 充值成功最大金额 · 可空 |
| `withdrawal_cnt` | int | 提现尝试总次数 · 可空 |
| `withdrawal_s_cnt` | int | 提现成功次数 · 可空 |
| `withdrawal_amt` | decimal(15, 4) | 提现尝试总金额 · 可空 |
| `withdrawal_s_amt` | decimal(15, 4) | 提现成功金额 · 可空 |
| `withdrawal_max` | decimal(15, 4) | 提现尝试最大金额 · 可空 |
| `withdrawal_s_max` | decimal(15, 4) | 提现成功最大金额 · 可空 |
| `transfer_cnt` | int | 转账尝试总次数 · 可空 |
| `transfer_s_cnt` | int | 转账成功次数 · 可空 |
| `transfer_amt` | decimal(15, 4) | 转账尝试总金额 · 可空 |
| `transfer_s_amt` | decimal(15, 4) | 转账成功金额 · 可空 |
| `transfer_max` | decimal(15, 4) | 转账尝试最大金额 · 可空 |
| `transfer_s_max` | decimal(15, 4) | 转账成功最大金额 · 可空 |
| `card_pay_cnt` | int | 卡支付尝试总次数 · 可空 |
| `card_pay_s_cnt` | int | 卡支付成功次数 · 可空 |
| `card_pay_amt` | decimal(15, 4) | 卡支付尝试总金额 · 可空 |
| `card_pay_s_amt` | decimal(15, 4) | 卡支付成功金额 · 可空 |
| `repayment_s_cnt` | int | 还款成功次数 · 可空 |
| `repayment_s_amt` | decimal(15, 4) | 还款成功金额 · 可空 |
| `devices` | varchar(512) | 登录设备 deviceId1,deviceId2 · 可空 |
| `transfer_payee` | varchar(512) | 转账收款方信息 payeeId1:金额，payeeId2:金额 · 可空 |
| `last_trade_time` | datetime | 最后一次交易时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_trade_report_member_id`:member_id, report_date

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
