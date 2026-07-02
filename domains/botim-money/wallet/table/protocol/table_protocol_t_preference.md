---
id: tbl_protocol_t_preference
object_type: Table
name: 用户偏好 (t_preference)
aliases: [t_preference, protocol.t_preference]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: protocol schema DDL
tags: [wallet, protocol]
sensitivity: normal
related_services: []
---

# 用户偏好 (t_preference)

## 用途
物理表 `protocol.t_preference`,主键 `id`。用户偏好。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID 同signInfo主键 |
| `preference_type` | varchar(20) | 偏好类型，如：优先扣款方式 |
| `sign_info_id` | bigint(35) | 签订协议ID |
| `content` | varchar(255) | 内容 · 可空 |
| `status` | varchar(5) | 状态 Y：有效，N：无效 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `memo` | varchar(255) | 备注 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
