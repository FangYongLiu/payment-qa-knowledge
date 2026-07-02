---
id: tbl_ppc_t_card_operate_record
object_type: Table
name: Card Operate Record (t_card_operate_record)
aliases: [t_card_operate_record, ppc.t_card_operate_record]
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

# Card Operate Record (t_card_operate_record)

## 用途
物理表 `ppc.t_card_operate_record`,主键 `id`。Card Operate Record。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | ID,前八后九 |
| `virtual_card_id` | bigint | Virtual Card ID |
| `operate_type` | varchar(10) | Operate Type: C=Close, L=Lock, UL=Unlock, R=Replace, AP=Activate Physical Card, SP=Set PIN, SSMC/SSMD=Set Spend Mode |
| `operate_source` | char(3) | Operate Source: U=User, YSE=YSE |
| `operate_result` | char | Operate Result: S=Success, F=Failure |
| `memo` | varchar(100) | Memo · 可空 |
| `trx_ref_no` | varchar(20) | Transaction Ref No: Processor associate · 可空 |
| `extension` | varchar(100) | Extension · 可空 |
| `device_id` | varchar(64) | Device ID · 可空 |
| `host_app` | varchar(32) | Host App · 可空 |
| `sdk_version` | varchar(32) | SDK Version · 可空 |
| `create_time` | timestamp(3) | Create time |
| `update_time` | timestamp(3) | Update time |

## 主键 / 索引
- 主键:`id`
- `idx_update_time_virtual_card_id`:update_time, virtual_card_id
- `idx_virtual_card_id`:virtual_card_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
