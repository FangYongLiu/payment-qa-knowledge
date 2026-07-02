---
id: tbl_transfer_t_friendship
object_type: Table
name: 好友关系 (t_friendship)
aliases: [t_friendship, transfer.t_friendship]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: transfer schema DDL
tags: [wallet, transfer]
sensitivity: normal
related_services: []
---

# 好友关系 (t_friendship)

## 用途
物理表 `transfer.t_friendship`,主键 `id`。好友关系。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `member_id` | varchar(32) | 会员编号 |
| `friend_mid` | varchar(32) | 好友会员id |
| `friend_default_pid` | varchar(32) | 好友默认会员平台 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
