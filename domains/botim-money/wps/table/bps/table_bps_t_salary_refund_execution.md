---
id: tbl_bps_t_salary_refund_execution
object_type: Table
name: 工资退款执行表 (t_salary_refund_execution)
aliases: [t_salary_refund_execution, bps.t_salary_refund_execution]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bps schema DDL
tags: [wps, bps]
sensitivity: normal
related_services: []
---

# 工资退款执行表 (t_salary_refund_execution)

## 用途
物理表 `bps.t_salary_refund_execution`,主键 `id`。工资退款执行表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `employee_id` | char(32) | 员工id |
| `salary_refund_command_id` | char(32) | 退款指令表id |
| `salary_load_command_id` | char(32) | 转账指令表id |
| `refund_target_type` | char(10) | 目标账户类型 |
| `refund_target_ref_id` | varchar(32) | 目标账户 |
| `refund_disbursal_type` | char(10) | 出账账户类型 |
| `refund_disbursal_account` | varchar(32) | 出账账户 |
| `amount` | decimal(11, 2) | 退款金额 |
| `status` | char(10) | 退款状态 |
| `refund_request_no` | varchar(32) | 退款编号 · 可空 |
| `product_code` | char(10) | 产品码 |
| `transfer_mode` | char(10) | 退款方式 |
| `origin_ID` | varchar(64) | 请求id |
| `origin_bulk_ID` | varchar(64) | 请求批次id |
| `maker_id` | varchar(25) | 创建者 · 可空 |
| `approver_id` | varchar(25) | 审批者 · 可空 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
