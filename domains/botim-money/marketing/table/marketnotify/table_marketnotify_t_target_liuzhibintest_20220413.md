---
id: tbl_marketnotify_t_target_liuzhibintest_20220413
object_type: Table
name: 消息推送用户列表 (t_target_liuzhibintest_20220413)
aliases: [t_target_liuzhibintest_20220413, marketnotify.t_target_liuzhibintest_20220413]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketnotify schema DDL
tags: [marketing, marketnotify]
sensitivity: normal
related_services: []
---

# 消息推送用户列表 (t_target_liuzhibintest_20220413)

## 用途
物理表 `marketnotify.t_target_liuzhibintest_20220413`,主键 `member_id`。消息推送用户列表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `member_id` | varchar(32) | 会员id |
| `status` | char | 状态：I=未处理，B=block,F=发送失败，S=发送成功 |
| `error_msg` | varchar(255) | 错误信息：错误信息 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`member_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
