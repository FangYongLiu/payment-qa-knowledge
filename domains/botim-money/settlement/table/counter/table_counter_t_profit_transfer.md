---
id: tbl_counter_t_profit_transfer
object_type: Table
name: 计提转账记录表 (t_profit_transfer)
aliases: [t_profit_transfer, counter.t_profit_transfer]
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

# 计提转账记录表 (t_profit_transfer)

## 用途
物理表 `counter.t_profit_transfer`,主键 `flow_id`。计提转账记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `flow_id` | bigint(17) | 主键流水ID |
| `voucher_no` | varchar(64) | 凭证编号 · 可空 |
| `cr_account_no` | varchar(64) | 贷方账号 会计利润商户 |
| `cr_account_name` | varchar(128) | 贷方账户名称 |
| `cr_member_id` | varchar(32) | 贷方会员号 |
| `dr_account_no` | varchar(64) | 借方账号 会计计提户 |
| `dr_account_name` | varchar(128) | 借方账户名称 |
| `dr_member_id` | varchar(32) | 借方会员号 |
| `biz_product_code` | varchar(16) | 业务产品码 |
| `amount` | decimal(15, 2) | 金额 |
| `currency` | varchar(3) | 币种 |
| `status` | varchar(8) | 状态 |
| `message` | varchar(255) | 响应信息 · 可空 |
| `memo` | varchar(255) | 附言Memo · 可空 |
| `creator` | varchar(64) | 创建人 · 可空 |
| `updater` | varchar(64) | 更新人 · 可空 |
| `oss_path` | varchar(255) | ufs文件地址 · 可空 |
| `extension` | varchar(1024) | 扩展信息 · 可空 |
| `gmt_create` | timestamp | 创建时间 · 可空 |
| `gmt_modified` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`flow_id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
