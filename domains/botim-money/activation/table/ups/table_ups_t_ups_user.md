---
id: tbl_ups_t_ups_user
object_type: Table
name: 用户标识 (t_ups_user)
aliases: [t_ups_user, ups.t_ups_user]
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

# 用户标识 (t_ups_user)

## 用途
物理表 `ups.t_ups_user`,主键 `id`。用户标识。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识 |
| `guid` | varchar(64) | 全局标识 |
| `origin_country` | varchar(32) | 原出生国家 |
| `origin_region` | varchar(64) | 原出生地区 |
| `origin_address` | varchar(256) | 原出生地址 |
| `origin_name` | varchar(256) | 原名称 |
| `origin_name_latin` | varchar(256) | 原名拉丁字母 |
| `origin_gender` | varchar(16) | 原性别 |
| `origin_skin` | varchar(16) | 原肤色 |
| `birth_date` | bigint | 出生日期 |
| `permanent_address` | varchar(256) | 常住地址 |
| `use_status` | varchar(64) | 使用状态。分active,inactive,merge |
| `create_time` | bigint | 创建时间 |
| `update_time` | bigint | 更新时间 |
| `enable_flag` | varchar(2) | 记录是否有效(未作废),Y有效，N为已作废 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
