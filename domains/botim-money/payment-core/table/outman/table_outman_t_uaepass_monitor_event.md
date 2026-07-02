---
id: tbl_outman_t_uaepass_monitor_event
object_type: Table
name: 监听事件表 (t_uaepass_monitor_event)
aliases: [t_uaepass_monitor_event, outman.t_uaepass_monitor_event]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: outman schema DDL
tags: [payment-core, outman]
sensitivity: normal
related_services: []
---

# 监听事件表 (t_uaepass_monitor_event)

## 用途
物理表 `outman.t_uaepass_monitor_event`,主键 `event_id`。监听事件表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `event_id` | bigint | 事件id · 可空 |
| `event_key` | varchar(128) | 事件主标志, 如：uaepass返回的requestId |
| `relation_key` | varchar(128) | 关联key，如：请求方的requestId或requestNo · 可空 |
| `main_type` | varchar(32) | 事件主类型 |
| `sub_type` | varchar(32) | 事件子类型 · 可空 |
| `status` | char | 执行状态：I=初始，C=callback，V=推送可视数据, G=get dv info，F=失败，S=成功，E=异常 |
| `expire_time` | datetime | 过期时间 · 可空 |
| `extension` | varchar(512) | 扩展信息 · 可空 |
| `message` | varchar(128) | 错误信息 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |
| `pop_id` | varchar(80) | Proof of Presentation ID · 可空 |
| `vc_id` | varchar(80) | VC ID · 可空 |
| `member_id` | varchar(20) | member id · 可空 |
| `file_tag` | varchar(50) | file tag · 可空 |

## 主键 / 索引
- 主键:`event_id`
- `uk_event_key_type_subtype`:event_key, main_type, sub_type (UNIQUE)
- `uk_relation_key_type_subtype`:relation_key, main_type, sub_type (UNIQUE)
- `idx_create_time`:create_time
- `idx_pop_id`:pop_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
