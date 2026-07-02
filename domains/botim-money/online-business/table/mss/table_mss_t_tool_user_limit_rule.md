---
id: tbl_mss_t_tool_user_limit_rule
object_type: Table
name: 用户限额限次规则 (t_tool_user_limit_rule)
aliases: [t_tool_user_limit_rule, mss.t_tool_user_limit_rule]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mss schema DDL
tags: [online-business, mss]
sensitivity: normal
related_services: []
---

# 用户限额限次规则 (t_tool_user_limit_rule)

## 用途
物理表 `mss.t_tool_user_limit_rule`,主键 `LIMIT_RULE_ID`。用户限额限次规则。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `LIMIT_RULE_ID` | int | 主键ID · 可空 |
| `tool_id` | int | 工具id · 可空 |
| `rule_type` | varchar(16) | 规则类型 限额，限次 |
| `limit_type` | varchar(16) | 限制类型 日，月，年，总计 |
| `rule_value` | varchar(512) | 规则value |
| `op` | varchar(16) | 比较方式 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`LIMIT_RULE_ID`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
