---
id: tbl_acquireii_t_promotion_info
object_type: Table
name: 优惠券信息表 (t_promotion_info)
aliases: [t_promotion_info, acquireii.t_promotion_info]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: acquireii schema DDL
tags: [online-business, acquireii]
sensitivity: normal
related_services: [svc_acquireii]
---

# 优惠券信息表 (t_promotion_info)

## 用途
物理表 `acquireii.t_promotion_info`,主键 `id`。优惠券信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 通用指令id |
| `applied_reward_id` | varchar(64) | appliedRewardId |
| `order_id` | bigint | 订单ID |
| `settle_flag` | varchar(32) | settleFlag |
| `created_time` | timestamp(3) | 创建时间 |

## 主键 / 索引
- 主键:`id`
- `i_pi_ct`:created_time
- `i_pi_oi`:order_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
