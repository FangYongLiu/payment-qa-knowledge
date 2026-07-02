---
id: tbl_device_t_multi_mer_channel
object_type: Table
name: 多商户设备渠道信息 (t_multi_mer_channel)
aliases: [t_multi_mer_channel, device.t_multi_mer_channel]
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

# 多商户设备渠道信息 (t_multi_mer_channel)

## 用途
物理表 `device.t_multi_mer_channel`,主键 `id`。多商户设备渠道信息。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `multi_mer_id` | bigint | 多商户id |
| `merchant_mid` | varchar(50) | 商户mid |
| `device_id` | bigint | 设备ID |
| `mid` | varchar(50) | 外部商户号 |
| `tid` | varchar(50) | 外部设备号 |
| `channel_code` | varchar(50) | 渠道编码 |
| `tpdu` | varchar(50) | TPDU · 可空 |
| `cvm_limit` | int | cvm_limit · 可空 |
| `store_id` | varchar(30) | 门店id · 可空 |
| `status` | varchar(32) | 状态 |
| `created_time` | timestamp | 创建时间 |
| `last_updated_time` | timestamp | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `uid_mid_tid`:merchant_mid, tid (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
