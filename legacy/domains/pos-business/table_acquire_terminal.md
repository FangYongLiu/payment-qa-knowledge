---
id: tbl_acquire_terminal
object_type: Table
domain: device-pos
status: archived
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_acquire_terminal.md
tags:
- 收单
- 终端
subdomain: null
module: null
sensitivity: normal
name: 收单终端表
aliases:
- t_acquire_terminal
- acquireii.t_acquire_terminal
related_services: []
related_tables:
- tbl_acquire_extension
- tbl_acquireii_t_acquire_order
- tbl_acquireii_t_card_info
- tbl_acquireii_t_fiserv_channel_param
- tbl_acquireii_t_payment_info
- tbl_acquireii_t_terminal_detail
related_scenarios:
- scn_acquire_product_apply
- scn_fiserv_test_tid_creation
- scn_merchant_transaction_db_check
- scn_payment_code_scanned_by_pos
- scn_payment_code_scanned_by_scanner
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
记录收单订单关联的**终端基础信息**，物理表名 `acquireii.t_acquire_terminal`，业务含义为收单终端。该表与 `t_terminal_detail` 同属终端维度信息存储，但字段更精简，用于不同业务场景下记录订单的终端归属（如 POS 扫码、Fiserv 终端构造等）。

## 在交易链路中的位置
- 属于 **acquireII 收单交易链路** 的辅助维度表，挂在主单 `t_acquire_order` 之下。
- 当一笔收单订单来源于 POS / 扫码枪 / 实体终端时，订单创建过程会写入本表，记录该笔交易归属的终端及门店信息。
- 与同链路的 `t_payment_info`、`t_card_info`、`t_acquire_extension` 等扩展表平级，共同围绕 `global_id` 描述一笔订单的完整上下文。

## 关键列
| 字段 | 类型 | 说明 |
|------|------|------|
| `global_id` | bigint | **主键**，对应订单 global_id，与 `t_acquire_order.global_id` 一致 |
| `terminal_id` | varchar(200) | 终端 ID（对应 POS 设备/扫码设备编号） |
| `terminal_type` | varchar(50) | 终端类型 |
| `store_id` | varchar(200) | 门店 ID |

## 主键/索引
- 主键：`global_id`
- 索引：
  - PRIMARY (global_id) — 主键

## 关联关系
- **`t_acquire_order` (1:1)**：通过 `global_id` 关联，本表为订单的终端维度扩展。
- **`t_terminal_detail`**：同样记录终端信息但字段更全，二者使用场景不同，需根据业务渠道区分写入。
- **`t_payment_info` / `t_card_info` / `t_acquire_extension`**：均以 `global_id` 与本表平级关联，组成完整订单视图。
- **`t_fiserv_channel_param`**：在 Fiserv 渠道场景下，`terminal_id` 可与 Fiserv TID 配置打通。

## 校验点 (QA 关注)
1. **与 `t_terminal_detail` 重复性**：明确两张表的写入条件与业务渠道差异，避免同一笔订单两边都写或都不写。
2. **terminal_id 关联 POS 设备**：核对 `terminal_id` 能正确映射到 POS / 扫码设备配置，尤其在 Fiserv TID 构造场景下需与渠道侧 TID 一致。
3. **1:1 一致性**：通过 `global_id` 与 `t_acquire_order` 1:1 关联，校验订单与终端记录一一对应，无孤儿记录。
4. **store_id 完整性**：门店 ID 必须能在商户/门店维度配置中查到，避免脏数据。
5. **terminal_type 枚举合法性**：核对终端类型取值范围与业务文档一致。

## 常用查询
```sql
-- 根据订单查终端
SELECT * FROM t_acquire_terminal WHERE global_id = ?;

-- 联合主单核对一致性
SELECT o.global_id, o.merchant_id, t.terminal_id, t.terminal_type, t.store_id
FROM t_acquire_order o
LEFT JOIN t_acquire_terminal t ON o.global_id = t.global_id
WHERE o.global_id = ?;
```
