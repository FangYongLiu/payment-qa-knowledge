---
id: tbl_ppc_t_fx_rate_version
object_type: Table
name: Foreign Exchange Rate Version (t_fx_rate_version)
aliases: [t_fx_rate_version, ppc.t_fx_rate_version]
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

# Foreign Exchange Rate Version (t_fx_rate_version)

## 用途
物理表 `ppc.t_fx_rate_version`,主键 `version_id`。Foreign Exchange Rate Version。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `version_id` | bigint | Version ID · 可空 |
| `currency_code` | char(3) | Currency Code |
| `selling_rate` | decimal(10, 4) | Selling Rate |
| `buying_rate` | decimal(10, 4) | Buying Rate |
| `bank_selling_rate` | decimal(10, 4) | Bank Selling Rate |
| `target_rate` | decimal(10, 6) | Target Rate · 可空 |
| `sync_status` | char | Sync Status: P=Processing, S=Success, F=Fail |
| `txn_ref_no` | varchar(20) | Txn Ref No · 可空 |
| `error_message` | varchar(100) | Error Message · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `operator` | varchar(50) | Operator |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`version_id`
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
