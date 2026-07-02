---
id: tbl_memberfront_t_member_logout_reason
object_type: Table
name: 会员护照信息表 (t_member_logout_reason)
aliases: [t_member_logout_reason, memberfront.t_member_logout_reason]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: memberfront schema DDL
tags: [activation, memberfront]
sensitivity: normal
related_services: []
---

# 会员护照信息表 (t_member_logout_reason)

## 用途
物理表 `memberfront.t_member_logout_reason`,主键 `id`。会员护照信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(32) | 主键 |
| `request_no` | varchar(32) | 请求编号 |
| `member_id` | varchar(32) | 会员编号 |
| `reason_id` | bigint(32) | 原因配置ID · 可空 |
| `reason_desc` | varchar(512) | 注销原因 · 可空 |
| `memo` | varchar(512) | 备注 · 可空 |
| `create_time` | timestamp | 建立时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
