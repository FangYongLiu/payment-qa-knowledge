---
id: tbl_ppc_t_sync_detail
object_type: Table
name: Sync Detail (t_sync_detail)
aliases: [t_sync_detail, ppc.t_sync_detail]
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

# Sync Detail (t_sync_detail)

## 用途
物理表 `ppc.t_sync_detail`,主键 `detail_id`。Sync Detail。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `detail_id` | bigint | Detail Id: 8 + 9 digits |
| `progress_id` | bigint | Progress Id |
| `virtual_card_id` | bigint | Virtual Card Id |
| `accounting_version` | bigint | Accounting Version · 可空 |
| `detail_type` | char(2) | Detail Type: I=Init Load, CL=Close Loop, OL=Open Loop, F=Freeze, UF=UnFreeze, M=Manual |
| `detail_status` | char | Detail Status: N=No Need, P=Processing, S=Success |
| `drcr` | char | DrCr Indicator: D=Debit, C=Credit |
| `amount` | decimal(19, 4) | Amount |
| `currency` | char(3) | Currency |
| `trx_ref_no` | varchar(12) | Trx Ref No · 可空 |
| `extension` | varchar(255) | Extension · 可空 |
| `create_time` | timestamp(3) | Create time |
| `update_time` | timestamp(3) | Update time |

## 主键 / 索引
- 主键:`detail_id`
- `idx_update_time_progress_id`:update_time, progress_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
