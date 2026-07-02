---
id: tbl_ppc_t_daily_balance_detail
object_type: Table
name: Daily Balance Detail (t_daily_balance_detail)
aliases: [t_daily_balance_detail, ppc.t_daily_balance_detail]
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

# Daily Balance Detail (t_daily_balance_detail)

## 用途
物理表 `ppc.t_daily_balance_detail`,主键 `detail_id`。Daily Balance Detail。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `detail_id` | bigint | Detail id: 8 digits date time + 9 digits sequence |
| `summary_id` | bigint | Summary id |
| `proxy_number` | varchar(20) | Proxy number |
| `file_balance` | decimal(19, 4) | File balance · 可空 |
| `file_card_status` | varchar(8) | File card status · 可空 |
| `check_balance_status` | char | Check balance status: I=Initial(more in file), S=Success, M=Mismatch, L=Lack(more at our side) |
| `check_card_status` | char | Check card status: I=Initial(more in file), S=Success, M=Mismatch, L=Lack(more at our side) |
| `mismatch_data` | varchar(200) | Mismatch data: JSON format: balance, status at our side · 可空 |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`detail_id`
- `uk_proxy_number_summary_id`:proxy_number, summary_id (UNIQUE)
- `idx_summary_id`:summary_id
- `idx_update_time`:update_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
