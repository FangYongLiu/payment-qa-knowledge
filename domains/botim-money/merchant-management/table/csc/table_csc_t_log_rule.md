---
id: tbl_csc_t_log_rule
object_type: Table
name: 日志匹配规则 (t_log_rule)
aliases: [t_log_rule, csc.t_log_rule]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: csc schema DDL
tags: [merchant-management, csc]
sensitivity: normal
related_services: []
---

# 日志匹配规则 (t_log_rule)

## 用途
物理表 `csc.t_log_rule`,主键 `id`。日志匹配规则。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | ID · 可空 |
| `function_code` | varchar(32) | 功能: porter_cgs,porter_sgs · 可空 |
| `rule_type` | varchar(32) | 规则类型: 黑名单=BLACK,白名单=WHITE · 可空 |
| `app_code` | varchar(64) | 系统编码 · 可空 |
| `api_code` | varchar(128) | api · 可空 |
| `return_code` | varchar(32) | 返回码 · 可空 |
| `expression_type` | varchar(32) | 表达式类型: 正则=REGEX，全文匹配=TEXT,空白=NONE |
| `match_expression` | varchar(255) | 匹配表达式: 返回消息匹配表达式 · 可空 |
| `enable_flag` | char | 启用标识: Y=启用，N=停用 |
| `update_by` | varchar(32) | 最后修改人 · 可空 |
| `memo` | varchar(100) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
