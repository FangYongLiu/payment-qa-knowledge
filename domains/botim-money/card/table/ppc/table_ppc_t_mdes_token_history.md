---
id: tbl_ppc_t_mdes_token_history
object_type: Table
name: MDES Token history (t_mdes_token_history)
aliases: [t_mdes_token_history, ppc.t_mdes_token_history]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ppc schema DDL
tags: [card, ppc]
sensitivity: normal
related_services: []
---

# MDES Token history (t_mdes_token_history)

## 用途
物理表 `ppc.t_mdes_token_history`,主键 `token_history_id`。MDES Token history。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `token_history_id` | bigint | Token History ID |
| `token_id` | bigint | Token ID |
| `before_token_status` | varchar(8) | Token Status: TA=Token Activating, AC=Activating Completed, A=Active, S=Suspended, D=Deleted |
| `token_status` | varchar(8) | Token Status: TA=Token Activating, AC=Activating Completed, A=Active, S=Suspended, D=Deleted |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create Time |

## 主键 / 索引
- 主键:`token_history_id`
- `idx_create_time_token_id`:create_time, token_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
