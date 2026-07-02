---
id: tbl_protocol_t_contract_expired_record
object_type: Table
name: t_contract_expired_record (t_contract_expired_record)
aliases: [t_contract_expired_record, protocol.t_contract_expired_record]
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

# t_contract_expired_record (t_contract_expired_record)

## 用途
物理表 `protocol.t_contract_expired_record`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(12) | 主键 · 可空 |
| `user_id` | varchar(32) | 用户ID |
| `sign_contract_no` | varchar(25) | 待补 · 可空 |
| `contract_sub_type` | varchar(32) | 待补 · 可空 |
| `status` | tinyint(1) | 1:已重签；0:待重签； · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `IDX_CONTRACT_CREATE_TIME`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
