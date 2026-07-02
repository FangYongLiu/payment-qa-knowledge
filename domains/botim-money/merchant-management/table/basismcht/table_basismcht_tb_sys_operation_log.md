---
id: tbl_basismcht_tb_sys_operation_log
object_type: Table
name: 操作日志 (tb_sys_operation_log)
aliases: [tb_sys_operation_log, basismcht.tb_sys_operation_log]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basismcht schema DDL
tags: [merchant-management, basismcht]
sensitivity: normal
related_services: []
---

# 操作日志 (tb_sys_operation_log)

## 用途
物理表 `basismcht.tb_sys_operation_log`,主键 `operation_log_id`。操作日志。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `operation_log_id` | bigint | 主键 |
| `log_type` | varchar(32) | 日志类型(字典) · 可空 |
| `log_name` | varchar(255) | 日志名称 · 可空 |
| `user_id` | bigint(65) | 用户id · 可空 |
| `class_name` | varchar(255) | 类名称 · 可空 |
| `method` | text | 方法名称 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `succeed` | varchar(32) | 是否成功(字典) · 可空 |
| `message` | text | 备注 · 可空 |
| `merchant_mid` | varchar(32) | Merchant Mid · 可空 |
| `staff_mid` | varchar(32) | Staff Mid · 可空 |
| `menu_id` | bigint | 菜单ID · 可空 |

## 主键 / 索引
- 主键:`operation_log_id`
- `idx_merchant_mid`:merchant_mid
- `idx_staff_mid`:staff_mid

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
