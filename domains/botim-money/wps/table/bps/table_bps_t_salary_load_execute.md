---
id: tbl_bps_t_salary_load_execute
object_type: Table
name: 工资转账表 (t_salary_load_execute)
aliases: [t_salary_load_execute, bps.t_salary_load_execute]
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

# 工资转账表 (t_salary_load_execute)

## 用途
物理表 `bps.t_salary_load_execute`,主键 `id`。工资转账表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `command_id` | char(32) | 工资转账指令请求id |
| `corporate_id` | char(32) | 公司id · 可空 |
| `corporate_name` | varchar(255) | 公司名称 · 可空 |
| `employee_id` | char(32) | 员工id · 可空 |
| `employee_full_name` | varchar(250) | employee full name · 可空 |
| `salary_load_type` | varchar(32) | 出转类型 |
| `loading_source` | varchar(64) | 出帐标识 |
| `load_target_type` | varchar(32) | 入帐类型 |
| `load_target_ref_id` | varchar(64) | 入帐标识 |
| `disbursal_type` | varchar(32) | 出帐账户类型 |
| `disbursal_account` | varchar(64) | 出帐账户 |
| `transfer_mode` | varchar(32) | 转账类型 |
| `load_amount` | decimal(11, 2) | 转帐金额 |
| `income_fixed` | decimal(11, 2) | 固定工资 |
| `income_variable` | decimal(11, 2) | 变动工资 |
| `pay_start_date` | varchar(32) | 转账开始日期 |
| `pay_end_date` | varchar(32) | 转账结束日期 |
| `days_on_leave` | int | 假期天数 · 可空 |
| `days_in_period` | int | 发薪周期 |
| `employer_ID` | varchar(32) | 雇佣者 |
| `paf_file_id` | varchar(32) | wps 转账文件id · 可空 |
| `product_code` | char(6) | 转账产品码 · 可空 |
| `salary_loading_remark` | varchar(128) | 转账备注 · 可空 |
| `status` | varchar(32) | 转账状态 |
| `origin_ID` | varchar(64) | 请求id |
| `origin_bulk_ID` | varchar(64) | 请求批次id |
| `trade_request_no` | varchar(64) | 转账流水号 · 可空 |
| `vendor_sync_status` | varchar(32) | yse同步状态 · 可空 |
| `maker_id` | varchar(25) | 创建者 · 可空 |
| `approve_id` | varchar(25) | 审批者 · 可空 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
