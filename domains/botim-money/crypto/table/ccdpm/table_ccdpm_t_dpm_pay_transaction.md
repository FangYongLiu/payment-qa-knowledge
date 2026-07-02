---
id: tbl_ccdpm_t_dpm_pay_transaction
object_type: Table
name: 记账事务 (t_dpm_pay_transaction)
aliases: [t_dpm_pay_transaction, ccdpm.t_dpm_pay_transaction]
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

# 记账事务 (t_dpm_pay_transaction)

## 用途
物理表 `ccdpm.t_dpm_pay_transaction`,主键 `transaction_id`。记账事务。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `transaction_id` | varchar(32) | 事务ID |
| `package_no` | varchar(32) | 包号：批量入帐时用 · 可空 |
| `transaction_no` | varchar(32) | 记账事务号：全局唯一，8位日期(yyyyMMdd) + 9位序列号 + 2位系统编号 |
| `app_id` | varchar(32) | 应用ID · 可空 |
| `sys_trace_no` | varchar(32) | 系统跟踪号：全局唯一，和记账事务号相同或者从凭证服务获取 · 可空 |
| `txn_type` | decimal(1) | 事务类型：0:正常,1:红字,2:蓝字,9:抹帐 |
| `product_code` | varchar(12) | 产品码 · 可空 |
| `pay_code` | varchar(12) | 支付编码 · 可空 |
| `status` | decimal(1) | 状态：0:初始,1:处理中,2:入账完成(成功) ,3:入账失败,处理中,4:入账完成(失败) |
| `accounting_date` | varchar(8) | 会计日 |
| `create_time` | timestamp | 插入时间 |
| `last_update_time` | timestamp | 更新时间 · 可空 |
| `remark` | varchar(256) | 备注 · 可空 |
| `context_trans_no` | varchar(32) | 关联事务号：回滚用 · 可空 |

## 主键 / 索引
- 主键:`transaction_id`
- `uk_transaction_no`:transaction_no (UNIQUE)
- `idx_sys_trace_no`:sys_trace_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
