---
id: tbl_memberfront_t_apply
object_type: Table
name: 申请表 (t_apply)
aliases: [t_apply, memberfront.t_apply]
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

# 申请表 (t_apply)

## 用途
物理表 `memberfront.t_apply`,主键 `id`。申请表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(32) | 主键 |
| `request_no` | varchar(32) | 请求编号 |
| `apply_type` | varchar(32) | 申请类型 |
| `member_id` | varchar(32) | 申请人 |
| `mobile` | varchar(32) | 申请人手机号 · 可空 |
| `source_code` | varchar(50) | 申请来源 · 可空 |
| `status` | varchar(25) | 状态 |
| `buffer_time` | datetime | 缓冲执行日期 · 可空 |
| `host_app` | varchar(50) | 宿主平台 · 可空 |
| `notify_flag` | varchar(5) | 是否通知（N：未通知，S：通知成功，F：通知失败） · 可空 |
| `memo` | varchar(512) | 备注 · 可空 |
| `create_time` | timestamp | 建立时间 |
| `update_time` | timestamp | 更新时间 |
| `email` | varchar(50) | 电子邮件 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_buffer_time`:buffer_time
- `idx_mid`:member_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
