---
id: tbl_reconciliation_t_on_account_detail
object_type: Table
name: 挂账明细表 (t_on_account_detail)
aliases: [t_on_account_detail, reconciliation.t_on_account_detail]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: reconciliation schema DDL
tags: [settlement, reconciliation]
sensitivity: normal
related_services: []
---

# 挂账明细表 (t_on_account_detail)

## 用途
物理表 `reconciliation.t_on_account_detail`,主键 `id`。挂账明细表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `summary_id` | bigint | 汇总Id |
| `on_account_type` | char | 挂账类型 O:挂账 W:销账 |
| `sub_type` | varchar(32) | 挂销账子类型 · 可空 |
| `debit_account` | varchar(32) | 借方账户 |
| `dr_member_id` | varchar(20) | 借方会员ID |
| `credit_account` | varchar(32) | 贷方账户 |
| `cr_member_id` | varchar(20) | 贷方会员ID |
| `amount` | decimal(19, 4) | 金额 |
| `currency` | char(3) | 币种 |
| `accounting_voucher_no` | varchar(32) | 登账凭证 · 可空 |
| `file_name` | varchar(255) | 文件名称 · 可空 |
| `operator` | varchar(32) | 操作人 · 可空 |
| `status` | char | 状态 P:处理中 F:失败 S:成功 |
| `result_message` | varchar(255) | 结果信息 · 可空 |
| `notify_status` | char | 通知状态 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `extension` | varchar(512) | 扩展字段 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `uk_accountVoucherNo`:accounting_voucher_no (UNIQUE)
- `idx_summaryId`:summary_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
