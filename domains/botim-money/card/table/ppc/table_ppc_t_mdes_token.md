---
id: tbl_ppc_t_mdes_token
object_type: Table
name: MDES Token (t_mdes_token)
aliases: [t_mdes_token, ppc.t_mdes_token]
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

# MDES Token (t_mdes_token)

## 用途
物理表 `ppc.t_mdes_token`,主键 `token_id`。MDES Token。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `token_id` | bigint | Token ID |
| `token_no` | varchar(100) | Token Number Associated with the device/Card |
| `agent_type` | varchar(10) | Agent Type: GP=Google Pay, SP=Samsung Pay, AP=Apple Pay |
| `proxy_number` | varchar(12) | Proxy Number |
| `device_name` | varchar(100) | Device Name Associated with the Token Number · 可空 |
| `device_id` | varchar(100) | Device ID Number Associated with the Token Number · 可空 |
| `token_status` | varchar(8) | Token Status: TA=Token Activating, AC=Activating Completed, A=Active, S=Suspended, D=Deleted |
| `txn_ref_no` | varchar(50) | Unique Transaction Reference · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `request_date` | timestamp | Token Request Date · 可空 |
| `expiry_time` | timestamp | Token Expiry · 可空 |
| `create_time` | timestamp | Create Time |
| `update_time` | timestamp | Update Time |
| `pan_unique_reference` | varchar(100) | Pan Unique Reference · 可空 |

## 主键 / 索引
- 主键:`token_id`
- `idx_pan_unique_reference`:pan_unique_reference
- `idx_proxy_number_status`:proxy_number, token_status
- `idx_token_no`:token_no

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
