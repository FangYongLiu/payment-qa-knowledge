---
id: tbl_protocol_t_contract_template
object_type: Table
name: t_contract_template (t_contract_template)
aliases: [t_contract_template, protocol.t_contract_template]
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

# t_contract_template (t_contract_template)

## 用途
物理表 `protocol.t_contract_template`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 待补 · 可空 |
| `contract_name` | varchar(100) | 协议名称 |
| `contract_type` | varchar(25) | 协议类型 |
| `contract_sub_type` | varchar(32) | 协议子类型 |
| `sign_relation` | varchar(25) | 签订关系，如两方，三方 |
| `contract_no` | varchar(25) | 协议编号 |
| `version` | varchar(10) | 协议版本号 |
| `description` | varchar(255) | 协议说明 |
| `period` | varchar (15) | 周期时长 1Y2M3D · 可空 |
| `renew_flag` | varchar(5) | 是否自动续约 |
| `terminate_flag` | varchar(5) | 是否可解约 |
| `notify_flag` | varchar(5) | 是否可通知 |
| `status` | varchar(5) | 状态，Y:有效，N：无效 |
| `lang_type` | varchar(10) | 语言类型 · 可空 |
| `extension` | text | 拓展字段 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `memo` | varchar(255) | 备注 · 可空 |
| `resign_type` | varchar(32) | 是否重签：IGNORE（无需重签）UPGRADE（升级重签）EXPIRED（过期重签）COMPREHENSIVE(重签) · 可空 |
| `force_sign_type` | varchar(32) | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
