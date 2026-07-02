---
id: tbl_activity_t_msg_template
object_type: Table
name: 通知模版表#记录通知模版#新增模版或要修改已有模版时要新增或修改记录#yanghuilong (t_msg_template)
aliases: [t_msg_template, activity.t_msg_template]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: activity schema DDL
tags: [marketing, activity]
sensitivity: normal
related_services: []
---

# 通知模版表#记录通知模版#新增模版或要修改已有模版时要新增或修改记录#yanghuilong (t_msg_template)

## 用途
物理表 `activity.t_msg_template`,主键 `id`。通知模版表#记录通知模版#新增模版或要修改已有模版时要新增或修改记录#yanghuilong。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `msg_type` | smallint(4) | 消息的类型：1：纯文本正文，只看content字段，2、纯文本 标题+正文，关注title,content两个字段,3、HTML 标题+正文，关注title,content两个字段,前端显示时需要对内容做html处理或渲染 |
| `title` | varchar(64) | 标题 · 可空 |
| `content` | varchar(4096) | 消息 · 可空 |
| `button_text` | varchar(64) | 按钮文案 · 可空 |
| `button_link` | varchar(255) | 按钮跳转链接 · 可空 |
| `param_list` | varchar(255) | 模版中通配符参数名list，参数名之间用英文的逗号分割 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
