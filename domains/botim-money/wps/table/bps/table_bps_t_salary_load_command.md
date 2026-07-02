---
id: tbl_bps_t_salary_load_command
object_type: Table
name: 工资转账指令表 (t_salary_load_command)
aliases: [t_salary_load_command, bps.t_salary_load_command]
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

# 工资转账指令表 (t_salary_load_command)

## 用途
物理表 `bps.t_salary_load_command`,主键 `id`。工资转账指令表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `corporate_reg_id` | varchar(100) | 公司注册id |
| `employee_reg_id` | varchar(100) | 员工注册id |
| `routing_code` | varchar(32) | 路由编号 |
| `iban` | varchar(64) | 卡号 |
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
| `remark` | varchar(128) | 转账备注 · 可空 |
| `status` | varchar(32) | 转账状态 |
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
