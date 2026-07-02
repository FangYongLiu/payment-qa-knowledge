---
id: tbl_callcenter_t_extension_info
object_type: Table
name: 分机信息表 (t_extension_info)
aliases: [t_extension_info, callcenter.t_extension_info]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: callcenter schema DDL
tags: [merchant-management, callcenter]
sensitivity: normal
related_services: []
---

# 分机信息表 (t_extension_info)

## 用途
物理表 `callcenter.t_extension_info`,主键 `id`。分机信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `ext_num` | varchar(32) | 分机号 |
| `status` | smallint | 待补 |
| `queue_num` | varchar(32) | 所属队列号 · 可空 |
| `join_queue_pw` | varchar(32) | 加入到队列需要的密码 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 待补 |

## 主键 / 索引
- 主键:`id`
- `uk_ext`:ext_num (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
