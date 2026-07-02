---
id: tbl_ppc_t_fx_rate_config
object_type: Table
name: Foreign Exchange Rate Config (t_fx_rate_config)
aliases: [t_fx_rate_config, ppc.t_fx_rate_config]
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

# Foreign Exchange Rate Config (t_fx_rate_config)

## 用途
物理表 `ppc.t_fx_rate_config`,主键 `currency_code`。Foreign Exchange Rate Config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `currency_code` | char(3) | Currency Code |
| `current_version_id` | bigint | Current Version ID · 可空 |
| `syncing_version_id` | bigint | Syncing Version ID · 可空 |
| `min_rate` | decimal(10, 4) | Min Rate |
| `max_rate` | decimal(10, 4) | Max Rate |
| `enable_flag` | char | Enable Flag: Y=Yes，N=No |
| `popular_flag` | char | Popular Flag: Y=Yes，N=No |
| `show_priority` | bigint | Show priority |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`currency_code`
- `uk_currency_code`:currency_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
