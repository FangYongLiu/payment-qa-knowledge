---
id: tbl_bps_t_salary_refund_trade_request
object_type: Table
name: 工资退款请求记录表 (t_salary_refund_trade_request)
aliases: [t_salary_refund_trade_request, bps.t_salary_refund_trade_request]
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

# 工资退款请求记录表 (t_salary_refund_trade_request)

## 用途
物理表 `bps.t_salary_refund_trade_request`,主键 `id`。工资退款请求记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `employee_id` | char(32) | 员工id |
| `refund_request_no` | varchar(32) | 退款编号 |
| `refund_voucher_no` | varchar(32) | 退款返回号 · 可空 |
| `refund_execution_id` | char(32) | 退款执行表id |
| `refund_amount` | decimal(11, 2) | 退款金额 |
| `status` | char(10) | 退款状态 |
| `message` | varchar(100) | 退款信息 · 可空 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
