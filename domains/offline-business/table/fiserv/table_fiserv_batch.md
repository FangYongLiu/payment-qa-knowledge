---
id: tbl_fiserv_batch
object_type: Table
name: Fiserv批次表(acquireii.t_fiserv_batch)
aliases:
- t_fiserv_batch
- acquireii.t_fiserv_batch
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-06-25'
source_type: upload
source_ref: tables/t_fiserv_batch.md
tags:
- fiserv
- 批次
- 收单
related_services: [svc_acquireii]
related_scenarios: []
---

# Fiserv批次表(acquireii.t_fiserv_batch)

## 用途
`acquireii.t_fiserv_batch` 是 Fiserv 国际收单渠道的批次管理表，按设备维度组织结算批次。Fiserv 采用批次结算模式:每个 POS 设备在一段时间内的交易组成一个批次(Batch)，批次结束后统一上送 Fiserv 进行清算。一个 `device_id` 同时只能有一个开放(活跃)批次。本表是 Fiserv 渠道交易归集的**锚点**:所有 Fiserv 交易明细通过 `device_id` + 交易时间区间与该表绑定，批次关闭后驱动下游结算([[tbl_pos_settlement]] / [[tbl_pos_settlement_history]])。

库表:`acquireii.t_fiserv_batch`。链路:设备激活 → 打开批次(本表) → 销售/退款/撤销/冲正各订单表 → 关闭批次(end_time 落地) → 上送 Fiserv 清算 → POS 结算。

## 关联关系
- **所属服务**:[[svc_acquireii]](= frontmatter `related_services`,tbl→service 边)。
- **关键表**:[[tbl_fiserv_sale_order]] / [[tbl_fiserv_refund_order]] / [[tbl_fiserv_sale_void_ops_order]] / [[tbl_fiserv_reversal_order]](`device_id` + 时间区间归集批内交易)、[[tbl_merchant_device]](`device_id` 设备所属商户)、[[tbl_hardware_info]](`device_id` 设备硬件)、[[tbl_pos_settlement]] / [[tbl_pos_settlement_history]](批次关闭后驱动结算)。
- **哪些场景校验它**:POS 刷卡交易落库检查([[scn_pos_transaction_db_check]])。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `batch_id` | bigint ✅ | 主键，批次 ID |
| `device_id` | varchar(32) ✅ | 设备 ID(唯一约束，关联 [[tbl_merchant_device]] / [[tbl_hardware_info]]) |
| `partner_id` | varchar(32) ✅ | 商户 ID |
| `start_time` | timestamp(3) ✅ | 批次开始时间 |
| `end_time` | timestamp(3) ✅ | 批次结束时间 |
| `created_time` / `last_updated_time` | timestamp(3) ✅ | 创建/更新时间 |
| `data_version` | bigint ✅ | 数据版本(乐观锁) |

## 主键 / 索引
- 主键:`batch_id`。
- 索引:`uk_fb_device`(device_id，唯一约束——一个设备一个活跃批次)、`i_fb_lut`(last_updated_time，增量同步)。

## 校验点(QA 关注)
- **device_id 唯一约束**:一个设备同时只能存在一个活跃批次，重复创建应被 `uk_fb_device` 拒绝。
- **批次范围**:批次内交易由 `device_id` + 时间区间确定，关联交易明细 `created_time BETWEEN start_time AND end_time`。
- **批次关闭后不可再加入交易**:`end_time` 落地后新交易不应再归属该批次，需新开批次。
- **时间一致性**:`start_time ≤ end_time`、`created_time ≤ last_updated_time`，批内每笔交易 `created_time` 必须在区间内。
- **data_version**:批次状态更新(如关闭)通过乐观锁递增，验证并发不脏写。
- **跨表对账**:[[tbl_fiserv_sale_order]] 等明细的 `device_id` 必须能在本表找到匹配批次，否则视为孤儿交易。
- **测试构造**:测试环境创建 device 与初始批次的方法待补(参见 Fiserv TID 构造相关场景)。
