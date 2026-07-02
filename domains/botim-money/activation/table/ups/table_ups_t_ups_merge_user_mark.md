---
id: tbl_ups_t_ups_merge_user_mark
object_type: Table
name: 合并用户标识 记录 (t_ups_merge_user_mark)
aliases: [t_ups_merge_user_mark, ups.t_ups_merge_user_mark]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ups schema DDL
tags: [activation, ups]
sensitivity: normal
related_services: []
---

# 合并用户标识 记录 (t_ups_merge_user_mark)

## 用途
物理表 `ups.t_ups_merge_user_mark`,主键 `id`。合并用户标识 记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识 |
| `guid` | varchar(64) | 全局标识 |
| `target_guid` | varchar(64) | 被合并的guid，原会员的guid将换为此guid |
| `create_time` | bigint | 创建时间 |
| `update_time` | bigint | 更新时间 |
| `enable_flag` | varchar(2) | 记录是否有效(未作废),Y有效，N为已作废 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
