---
id: tbl_amlreport_tb_risk_case
object_type: Table
name: 风险案件信息 (tb_risk_case)
aliases: [tb_risk_case, amlreport.tb_risk_case]
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

# 风险案件信息 (tb_risk_case)

## 用途
物理表 `amlreport.tb_risk_case`,主键 `id`。风险案件信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `transaction_id` | varchar(64) | 交易ID · 可空 |
| `payment_order_no` | varchar(64) | 支付订单号 · 可空 |
| `member_id` | varchar(32) | 会员id · 可空 |
| `pay_amount` | decimal(15, 4) | 支付金额 · 可空 |
| `currency` | varchar(10) | 币种 · 可空 |
| `case_type` | varchar(50) | 案件类型 · 可空 |
| `status` | varchar(10) | 案件状态 · 可空 |
| `charge_back_status` | varchar(50) | 拒付处理状态 · 可空 |
| `control_status` | varchar(20) | 控制状态 · 可空 |
| `black_list` | varchar(255) | 黑名单 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `operator` | varchar(20) | 操作人 · 可空 |
| `create_time` | timestamp(3) | 创建时间 · 可空 |
| `update_time` | timestamp(3) | 修改时间 · 可空 |
| `member_mobile` | varchar(32) | 会员手机号 · 可空 |
| `card_no` | varchar(32) | 银行卡号 · 可空 |
| `ip` | varchar(20) | ip · 可空 |
| `device_id` | varchar(64) | 设备id · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_case_member_id`:member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
