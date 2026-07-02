---
id: tbl_activity_t_notify_record
object_type: Table
name: 通知记录表#记录已发放的通知#发放通知或通知状态发生变更时要新增或更新此表#yanghuilong (t_notify_record)
aliases: [t_notify_record, activity.t_notify_record]
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

# 通知记录表#记录已发放的通知#发放通知或通知状态发生变更时要新增或更新此表#yanghuilong (t_notify_record)

## 用途
物理表 `activity.t_notify_record`,主键 `id`。通知记录表#记录已发放的通知#发放通知或通知状态发生变更时要新增或更新此表#yanghuilong。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `member_id` | bigint(32) | 用户id |
| `status` | smallint(4) | 状态: 0:用户未读，1：用户已读，-1：用户删除 |
| `msg_content` | varchar(4096) | 发送通知时要填充到通知内容中的特定参数 · 可空 |
| `notify_result` | varchar(255) | 通知发送结果：OK：成功，;其他：发送失败的原因 |
| `uuid` | varchar(64) | 消息的唯一id |
| `create_time` | timestamp | 待补 |
| `upadte_time` | timestamp | 待补 |
| `msg_type` | smallint(4) | 通知内容 的类型：1：纯文本正文，只看content字段，2、纯文本 标题+正文，关注title,content两个字段,3、HTML标题+正文，同t_msg_template中的msg_type |
| `inform_way` | smallint(4) | 推广方式：1：短信、2、app站内信 |
| `inform_channel` | smallint(4) | 推广渠道：1：短信、2：cashnow native app |
| `notify_app_flag` | smallint(4) | 同t_notify_plan种的notify_app_flag字段 |

## 主键 / 索引
- 主键:`id`
- `ix_ctime`:create_time
- `ix_member_id`:member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
