---
id: tbl_commission_t_comm_config
object_type: Table
name: Commission Config (t_comm_config)
aliases: [t_comm_config, commission.t_comm_config]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: commission schema DDL
tags: [settlement, commission]
sensitivity: normal
related_services: []
---

# Commission Config (t_comm_config)

## 用途
物理表 `commission.t_comm_config`,主键 `comm_config_id`。Commission Config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `comm_config_id` | bigint | Commission Config id · 可空 |
| `sync_progress_id` | bigint | Sync progress id |
| `group_type` | varchar(10) | Group type: BPC=Biz product code, PSC=Product set code |
| `group_code` | varchar(50) | Group code |
| `payee_id` | varchar(20) | Payee id |
| `pay_channel` | varchar(10) | Pay channel |
| `effect_time` | timestamp | Effect time |
| `expire_time` | timestamp | Expire time |
| `member_id` | varchar(20) | Member id |
| `calculate_type` | varchar(10) | Calculate type: DEF=Default Rule |
| `calculate_expression` | varchar(1000) | Calculate expression |
| `current_version_id` | bigint | Config Current Version Id · 可空 |
| `commission_type` | varchar(10) | C/R · 可空 |
| `product_package_id` | bigint | Product Package Id · 可空 |
| `config_status` | char | Config status: Y=Enabled, N=Disabled, E=Error Disabled |
| `extension` | varchar(255) | Extension · 可空 |
| `memo` | varchar(100) | Memo · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`comm_config_id`
- `idx_sync_progress_id_effect_time`:sync_progress_id, effect_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
