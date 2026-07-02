---
id: tbl_bps_t_salary_trade_request
object_type: Table
name: 转账请求表 (t_salary_trade_request)
aliases: [t_salary_trade_request, bps.t_salary_trade_request]
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

# 转账请求表 (t_salary_trade_request)

## 用途
物理表 `bps.t_salary_trade_request`,主键 `id`。转账请求表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `trade_request_no` | varchar(64) | 转账流水号 |
| `salary_load_id` | varchar(64) | 转账主键 |
| `employ_id` | varchar(64) | 员工id |
| `trade_product_code` | varchar(16) | 转账产品号 |
| `trade_status` | varchar(10) | 转账状态 |
| `load_amount` | decimal(11, 2) | 转账金额 |
| `message` | varchar(255) | 备注 · 可空 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
