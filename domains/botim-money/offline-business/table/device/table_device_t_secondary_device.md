---
id: tbl_device_t_secondary_device
object_type: Table
name: 二级商户设备 (t_secondary_device)
aliases: [t_secondary_device, device.t_secondary_device]
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

# 二级商户设备 (t_secondary_device)

## 用途
物理表 `device.t_secondary_device`,主键 `id`。二级商户设备。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `merchant_mid` | varchar(50) | 商户mid |
| `secondary_merchant_no` | varchar(50) | 二级商户号 |
| `secondary_terminal_no` | varchar(50) | 二级商户号 |
| `secondary_store_no` | varchar(64) | 二级门店号 · 可空 |

## 主键 / 索引
- 主键:`id`
- `udx_s_terminal_no`:secondary_terminal_no, merchant_mid (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
