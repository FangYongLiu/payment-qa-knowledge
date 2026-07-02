---
id: tbl_credit_t_cs_order
object_type: Table
name: 订单表 (t_cs_order)
aliases: [t_cs_order, credit.t_cs_order]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: credit schema DDL
tags: [lending, credit]
sensitivity: normal
related_services: []
---

# 订单表 (t_cs_order)

## 用途
物理表 `credit.t_cs_order`,主键 `id`。订单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键 · 可空 |
| `status` | int | 状态 |
| `loan_amount` | decimal(15, 2) | 借款金额 |
| `user_id` | varchar(50) | 用户ID |
| `credit_id` | int | 授信ID |
| `identity` | varchar(100) | 身份证 |
| `vendor` | varchar(50) | BANK/ACCOUNT/EXPAND_ORDER/RESTRUCTURE_ORDER/DEFERRAL_ORDER · 可空 |
| `period` | smallint (5) | 借款期限 |
| `period_unit` | smallint(5) | 期限单位：0 天 1 月 2年 |
| `loan_time` | timestamp | 放款时间 · 可空 |
| `apply_fund_time` | timestamp | 向资金方提交放款时间 · 可空 |
| `rebate` | int(5) | 借款利率 |
| `penalty` | int(5) | 罚息利率 |
| `finish_repay_time` | timestamp | 实际还款时间 · 可空 |
| `last_modified` | timestamp | 修改时间 · 可空 |
| `created_time` | timestamp | 创建时间 · 可空 |
| `order_no` | varchar(64) | 订单唯一ID |
| `is_recommend` | smallint(5) | 是否为推荐 · 可空 |
| `is_read` | smallint(2) | 状态已读未读 |
| `audit_start_time` | timestamp | 待补 · 可空 |
| `audit_finish_time` | timestamp | 待补 · 可空 |
| `product_code` | varchar(10) | 产品码 |
| `order_type` | tinyint(5) | order loan type 1:normal 2:expand 3:restructure 4:topUp |
| `loan_priority` | varchar(20) | 放款优先级 · 可空 |
| `ready_loan_time` | timestamp | 资金准备放款时间 · 可空 |
| `lenders` | varchar(20) | 资金方 |
| `price_tag` | varchar(255) | price tag · 可空 |
| `risk_tag` | varchar(255) | risk tag · 可空 |
| `fee` | decimal(15, 2) | 手续费 · 可空 |
| `ext` | varchar(255) | 扩展信息 · 可空 |
| `partner_id` | varchar(20) | 渠道 |
| `opt_in` | tinyint(5) | 0 不可发送营销  1可以发送营销 · 可空 |
| `cooling_off_waive` | tinyint(5) | 0 有冷静期  1无冷静期 · 可空 |
| `cooling_off_waive_time` | timestamp | 冷静期确认时间 · 可空 |
| `cooling_period_loan_cancel` | tinyint(5) | 冷静期取消订单 1 已取消 · 可空 |
| `cooling_period_loan_cancel_time` | timestamp | 冷静期取消订单时间 · 可空 |
| `cooling_off_period_finish` | tinyint(5) | 冷静期是否完成 1 完成 · 可空 |
| `cooling_off_period_finish_time` | timestamp | 冷静期完成时间 · 可空 |
| `cooling_off_waive_time_cancel_time` | timestamp | 冷静期间是否马上出款 · 可空 |
| `client_source` | varchar(32) | botim-remittance/h5/app/app-* · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_created_time`:created_time
- `idx_credit_id`:credit_id
- `idx_identity`:identity
- `idx_order_no`:order_no
- `idx_user_id`:user_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
