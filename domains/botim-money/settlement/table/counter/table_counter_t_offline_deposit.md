---
id: tbl_counter_t_offline_deposit
object_type: Table
name: 线下入金 (t_offline_deposit)
aliases: [t_offline_deposit, counter.t_offline_deposit]
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

# 线下入金 (t_offline_deposit)

## 用途
物理表 `counter.t_offline_deposit`,主键 `deposit_id`。线下入金。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `deposit_id` | bigint(17) | 存款id |
| `flow_id` | bigint(17) | 流水id |
| `payment_voucher_no` | varchar(32) | 支付凭证号 |
| `voucher_id` | bigint(17) | 凭证号 |
| `member_id` | varchar(32) | 会员id |
| `account_no` | varchar(32) | 借方账号 · 可空 |
| `status` | varchar(5) | 交易状态: I-初始、S-登账成功、F-登账失败 |
| `gmt_create` | timestamp | 创建时间 |
| `bill_status` | varchar(5) | 记账状态: I-初始、S-同步成功、F-同步失败 |
| `gmt_next_retry` | timestamp | 重试时间 · 可空 |
| `retry_count` | int | 重试次数 |
| `operator` | varchar(32) | 操作员名称 · 可空 |
| `apply_memo` | varchar(255) | 申请备注 · 可空 |
| `gmt_modified` | timestamp | 修改时间 |
| `result_msg` | varchar(128) | 登账响应信息 · 可空 |
| `notify_status` | varchar(4) | 线下入金通知状态 · 可空 |
| `notify_msg` | varchar(255) | 线下入金通知结果描述 · 可空 |
| `mns_template` | varchar(64) | 通知模板 · 可空 |
| `balance_status` | varchar(8) | 余额对账入账流水推送状态 · 可空 |
| `oss_path` | varchar(64) | ossPath 文件路径 · 可空 |

## 主键 / 索引
- 主键:`deposit_id`
- `idx_account_no`:account_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
