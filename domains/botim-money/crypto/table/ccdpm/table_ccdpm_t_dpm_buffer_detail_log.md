---
id: tbl_ccdpm_t_dpm_buffer_detail_log
object_type: Table
name: 待缓冲入账明细日志 (t_dpm_buffer_detail_log)
aliases: [t_dpm_buffer_detail_log, ccdpm.t_dpm_buffer_detail_log]
domain: crypto
status: active
owner: can.wang
reviewer: can.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ccdpm schema DDL
tags: [crypto, ccdpm]
sensitivity: normal
related_services: []
---

# 待缓冲入账明细日志 (t_dpm_buffer_detail_log)

## 用途
物理表 `ccdpm.t_dpm_buffer_detail_log`,主键 `buffer_detail_id`。待缓冲入账明细日志。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `buffer_detail_id` | bigint | 待入账数据流水号 |
| `account_no` | varchar(32) | 账户号 |
| `sys_trace_no` | varchar(32) | 系统跟踪号 · 可空 |
| `voucher_no` | varchar(50) | 凭证号 |
| `transaction_no` | varchar(32) | 事务号 |
| `currency` | varchar(10) | 币种 |
| `amount` | decimal(19, 8) | 金额 |
| `crdr` | decimal(1) | 借贷方向：1:借,2:贷 |
| `txn_type` | decimal(1) | 交易类型：0:正常,1:红字,2:蓝字,9:抹帐 |
| `accounting_rule` | decimal(1) | 记账规则：0:先贷后借(默认),1:借记,2:贷记 |
| `product_code` | varchar(12) | 支付产品编码 · 可空 |
| `pay_code` | varchar(12) | 支付编码 · 可空 |
| `summary` | varchar(256) | 摘要 · 可空 |
| `remark` | varchar(256) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `suite_no` | varchar(32) | 套号 |
| `context_voucher_no` | varchar(32) | 关联凭证号 · 可空 |
| `accounting_date` | varchar(8) | 会计日 · 可空 |
| `operation_type` | decimal(1) | 操作类型 · 可空 |
| `balance_type` | decimal(1) | 余额类型 · 可空 |

## 主键 / 索引
- 主键:`buffer_detail_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
