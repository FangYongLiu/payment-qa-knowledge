---
id: tbl_device_t_merchant_device
object_type: Table
name: 商户设备 (t_merchant_device)
aliases: [t_merchant_device, device.t_merchant_device]
domain: offline-business
status: active
owner: xiaoqian.wei,wanmei.ding
reviewer: xiaoqian.wei,wanmei.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: device schema DDL
tags: [offline-business, device]
sensitivity: normal
related_services: []
---

# 商户设备 (t_merchant_device)

## 用途
物理表 `device.t_merchant_device`,主键 `id`。商户设备。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 设备id · 可空 |
| `merchant_mid` | varchar(50) | 商户mid |
| `store_id` | bigint | 门店id · 可空 |
| `name` | varchar(64) | 设备名称 · 可空 |
| `hardware_id` | bigint | 硬件id |
| `active_code` | varchar(200) | 激活码 · 可空 |
| `status` | varchar(32) | 状态 ENABLE 可用 DISABLED 已停用 |
| `created_time` | timestamp | 创建时间 |
| `last_updated_time` | timestamp | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `secondary_device_id` | bigint | 二级设备id · 可空 |
| `last_report_gp_time` | timestamp | 最后上报坐标时间 · 可空 |
| `tips_type` | varchar(32) | 小费类型 · 可空 |
| `tips_max_amount` | decimal(19, 4) | 小费最大金额 · 可空 |
| `tips_currency` | varchar(3) | 小费币种 · 可空 |
| `tips_max_rate` | decimal(8, 6) | 小费最大比例 · 可空 |
| `tips_channel_code` | varchar(30) | tips 关联渠道 · 可空 |
| `borrow_store_Id` | bigint | 根据原t_secondary_terminal关系，绑定一级门店 · 可空 |
| `delivery_status` | varchar(20) | Device delivery status · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_device_code`:active_code (UNIQUE)
- `uk_device_sn`:hardware_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
