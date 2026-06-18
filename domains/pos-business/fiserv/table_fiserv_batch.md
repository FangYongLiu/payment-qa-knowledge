---
id: tbl_fiserv_batch
object_type: Table
domain: pos-business
status: active
owner: fangyong.liu@astratech.ae
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: upload
source_ref: tables/t_fiserv_batch.md
tags:
- fiserv
- 批次
- 收单
subdomain: fiserv
module: batch
sensitivity: normal
name: Fiserv批次表
aliases:
- t_fiserv_batch
- acquireii.t_fiserv_batch
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
Fiserv 渠道的批次管理表 `acquireii.t_fiserv_batch`，按设备维度组织结算批次。Fiserv 为国际收单渠道，采用批次结算模式：每个 POS 设备在一段时间内的交易组成一个批次，批次结束后统一上送 Fiserv 结算。

典型场景：
- POS 设备每天打烊时做一次批次结算
- 批次内所有交易一起对账
- 一个 device_id 同时只能有一个开放批次

通过 `device_id` 关联 Fiserv 相关订单表（sale / refund / void）。

## 关键列
| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `batch_id` | bigint | ✅ | 主键，批次 ID |
| `device_id` | varchar(32) | ✅ | 设备 ID（唯一约束） |
| `partner_id` | varchar(32) | ✅ | 商户 ID |
| `start_time` | timestamp(3) | ✅ | 批次开始时间 |
| `end_time` | timestamp(3) | ✅ | 批次结束时间 |
| `created_time` | timestamp(3) | ✅ | 创建时间 |
| `last_updated_time` | timestamp(3) | ✅ | 最后更新时间 |
| `data_version` | bigint | ✅ | 数据版本 |

## 主键/索引
| 索引名 | 字段 | 用途 |
|--------|------|------|
| PRIMARY | `batch_id` | 主键 |
| `uk_fb_device` | `device_id` | 唯一约束（一个设备一个活跃批次） |
| `i_fb_lut` | `last_updated_time` | 按更新时间查询 |

## 校验点(QA 关注)
1. **device_id 唯一约束**：一个设备同时只能有一个活跃批次，重复创建应被拒绝。
2. **批次范围由 start_time/end_time 划定**：批次内交易由 `device_id` + 时间范围（`s.created_time BETWEEN b.start_time AND b.end_time`）确定。
3. **批次关闭后不能再添加交易**。
4. 查询设备当前批次：`SELECT * FROM t_fiserv_batch WHERE device_id = ?;`
5. 关联交易明细需 JOIN `t_fiserv_sale_order`（及 refund / void）按 device_id + 时间范围匹配。
