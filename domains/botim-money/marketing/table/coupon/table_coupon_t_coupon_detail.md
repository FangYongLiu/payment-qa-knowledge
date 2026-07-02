---
id: tbl_coupon_t_coupon_detail
object_type: Table
name: 券明细表 (t_coupon_detail)
aliases: [t_coupon_detail, coupon.t_coupon_detail]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: coupon schema DDL
tags: [marketing, coupon]
sensitivity: normal
related_services: []
---

# 券明细表 (t_coupon_detail)

## 用途
物理表 `coupon.t_coupon_detail`,主键 `id`。券明细表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 |
| `coupon_id` | bigint | 券id |
| `coupon_code` | varchar(32) | 券码 |
| `status` | varchar(12) | 初始化：INIT；已使用：USED；已锁定：LOCKED |
| `secret_key` | varchar(64) | 密钥 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `idx_couponCode`:coupon_code
- `idx_coupon_id_status_updated_time`:coupon_id, status, updated_time
- `idx_created_time`:created_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
