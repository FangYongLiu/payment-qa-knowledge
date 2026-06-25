---
id: tbl_acquire_terminal
object_type: Table
name: 收单终端表(acquireii.t_acquire_terminal)
aliases:
- t_acquire_terminal
- acquireii.t_acquire_terminal
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: upload
source_ref: tables/t_acquire_terminal.md
tags:
- 收单
- 终端
related_services: [svc_acquireii]
related_scenarios: []
---

# 收单终端表(acquireii.t_acquire_terminal)

## 用途
记录收单订单关联的**终端基础信息**，物理表名 `acquireii.t_acquire_terminal`。该表与 [[tbl_acquireii_t_terminal_detail]] 同属终端维度信息存储，但字段更精简，用于不同业务场景下记录订单的终端归属(如 POS 扫码、Fiserv 终端构造等)。属于 acquireII 收单交易链路的辅助维度表，挂在主单 [[tbl_acquireii_t_acquire_order]] 之下，与 [[tbl_acquireii_t_payment_info]]、[[tbl_pcc_content]] 等扩展表平级，共同围绕 `global_id` 描述一笔订单的完整上下文。

库表:`acquireii.t_acquire_terminal`。

## 关联关系
- **所属服务**:[[svc_acquireii]](= frontmatter `related_services`,tbl→service 边)。
- **关键表**:[[tbl_acquireii_t_acquire_order]](`global_id` 1:1，本表为订单的终端维度扩展)、[[tbl_acquireii_t_terminal_detail]](字段更全，按业务渠道区分写入)、[[tbl_acquireii_t_payment_info]] / [[tbl_pcc_content]](`global_id` 平级关联)、[[tbl_acquireii_t_fiserv_channel_param]](Fiserv 场景 `terminal_id` 可与 Fiserv TID 配置打通)。
- **哪些场景校验它**:POS 刷卡交易落库检查([[scn_pos_transaction_db_check]]);另涉及商户交易落库检查、产品申请、付款码扫码等场景(对象待补)。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `global_id` | bigint | 主键，对应订单 global_id，与 [[tbl_acquireii_t_acquire_order]] 一致 |
| `terminal_id` | varchar(200) | 终端 ID(对应 POS 设备/扫码设备编号) |
| `terminal_type` | varchar(50) | 终端类型 |
| `store_id` | varchar(200) | 门店 ID |

## 主键 / 索引
- 主键:`global_id`(PRIMARY)。

## 校验点(QA 关注)
- **与 t_terminal_detail 重复性**:明确两张表的写入条件与业务渠道差异，避免同一笔订单两边都写或都不写。
- **terminal_id 关联 POS 设备**:核对 `terminal_id` 能正确映射到 POS / 扫码设备配置，尤其在 Fiserv TID 构造场景下需与渠道侧 TID 一致。
- **1:1 一致性**:通过 `global_id` 与 [[tbl_acquireii_t_acquire_order]] 1:1 关联，校验订单与终端记录一一对应，无孤儿记录。
- **store_id 完整性**:门店 ID 必须能在商户/门店维度配置中查到，避免脏数据。
- **terminal_type 枚举合法性**:核对终端类型取值范围与业务文档一致。
