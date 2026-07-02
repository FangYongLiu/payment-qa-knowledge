---
id: tbl_protocol_t_contract_sign_log
object_type: Table
name: 协议签订日志表 (t_contract_sign_log)
aliases: [t_contract_sign_log, protocol.t_contract_sign_log]
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

# 协议签订日志表 (t_contract_sign_log)

## 用途
物理表 `protocol.t_contract_sign_log`,主键 `id`。协议签订日志表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键ID |
| `log_type` | varchar(15) | 日志类型 |
| `user_id` | varchar(64) | User ID |
| `merchant_id` | varchar(25) | 商户ID · 可空 |
| `partner_id` | varchar(25) | 平台ID · 可空 |
| `source_id` | varchar(35) | 来源ID · 可空 |
| `sign_contract_no` | varchar(25) | 协议流水号 · 可空 |
| `package_id` | bigint | 协议包ID · 可空 |
| `contract_no` | varchar(25) | 模版协议编号 |
| `contract_version` | varchar(10) | 协议版本 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `memo` | varchar(255) | 备注 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
