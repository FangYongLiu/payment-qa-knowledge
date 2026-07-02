---
id: tbl_counter_tb_accounting
object_type: Table
name: tb_accounting (tb_accounting)
aliases: [tb_accounting, counter.tb_accounting]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: counter schema DDL
tags: [settlement, counter]
sensitivity: normal
related_services: []
---

# tb_accounting (tb_accounting)

## 用途
物理表 `counter.tb_accounting`,主键 `accounting_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `accounting_id` | bigint | 账户id |
| `dr_account_no` | varchar(32) | 借方帐号 · 可空 |
| `dr_member_id` | varchar(32) | 借方会员id · 可空 |
| `dr_fund_type` | varchar(10) | 借方资金类型 · 可空 |
| `cr_account_no` | varchar(32) | 贷方帐号 · 可空 |
| `cr_member_id` | varchar(32) | 贷方会员id · 可空 |
| `cr_fund_type` | varchar(10) | 贷方帐号类型 · 可空 |
| `amount` | decimal(17, 4) | 金额 · 可空 |
| `currency` | char(3) | 币种 · 可空 |
| `biz_no` | varchar(32) | 业务订单号 · 可空 |
| `status` | char | 状态 · 可空 |
| `memo` | varchar(256) | 备注 · 可空 |
| `result_message` | varchar(256) | 结果 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `operator` | varchar(32) | 申请者 · 可空 |
| `file_name` | varchar(255) | ufs 文件名称 · 可空 |
| `bill_memo` | varchar(256) | 通知账单内容 · 可空 |
| `balance_status` | varchar(8) | 余额对账入账流水推送状态 · 可空 |
| `bank_date` | timestamp | 银行交易时间 · 可空 |
| `bank_reference` | varchar(64) | 银行流水号 · 可空 |

## 主键 / 索引
- 主键:`accounting_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
