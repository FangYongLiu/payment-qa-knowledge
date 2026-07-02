---
id: tbl_csimple_t_follow_info
object_type: Table
name: 公众号关注记录表 (t_follow_info)
aliases: [t_follow_info, csimple.t_follow_info]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: csimple schema DDL
tags: [card, csimple]
sensitivity: normal
related_services: []
---

# 公众号关注记录表 (t_follow_info)

## 用途
物理表 `csimple.t_follow_info`,主键 `follow_id`。公众号关注记录表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `follow_id` | bigint(17) | 主键 |
| `partner_id` | varchar(32) | 平台ID |
| `uid` | varchar(32) | 用户uid |
| `status` | tinyint | 状态（0 - 已关注,1 - 取关） |
| `client_id` | varchar(50) | OAuth2授权，clint id |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`follow_id`
- `uk_follow_pid_u_c`:partner_id, uid, client_id (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
