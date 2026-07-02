---
id: tbl_device_t_receipt_info
object_type: Table
name: 小票商业信息 (t_receipt_info)
aliases: [t_receipt_info, device.t_receipt_info]
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

# 小票商业信息 (t_receipt_info)

## 用途
物理表 `device.t_receipt_info`,主键 `id`。小票商业信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `device_id` | varchar(50) | 设备id |
| `logo` | varchar(300) | logo |
| `pos_merchant_name` | varchar(200) | 商户名称 |
| `pos_merchant_addr1` | varchar(500) | 待补 · 可空 |
| `pos_merchant_addr2` | varchar(500) | 待补 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `last_updated_time` | timestamp | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `UDX_DEVICE_ID`:device_id (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
