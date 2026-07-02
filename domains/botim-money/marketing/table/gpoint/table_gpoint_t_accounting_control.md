---
id: tbl_gpoint_t_accounting_control
object_type: Table
name: 修改时间 (t_accounting_control)
aliases: [t_accounting_control, gpoint.t_accounting_control]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: gpoint schema DDL
tags: [marketing, gpoint]
sensitivity: normal
related_services: []
---

# 修改时间 (t_accounting_control)

## 用途
物理表 `gpoint.t_accounting_control`,主键 `account_control_id`。修改时间。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `account_control_id` | bigint | 账户控制ID：前八后九 |
| `control_id` | bigint | 控制ID |
| `account_no` | bigint | 账户号 |
| `control_type` | varchar(10) | 控制类型：O=支出，I=收入，F=冻结 |
| `do_amount` | decimal(19, 2) | 操作数量 |
| `undo_amount` | decimal(19, 2) | 反操作数量 |
| `create_time` | timestamp(3) | 创建时间 |
| `update_time` | timestamp(3) | 待补 |

## 主键 / 索引
- 主键:`account_control_id`
- `idx_update_time_account_no`:update_time, account_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
