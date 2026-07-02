---
id: tbl_device_t_device_channel
object_type: Table
name: 设备渠道 (t_device_channel)
aliases: [t_device_channel, device.t_device_channel]
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

# 设备渠道 (t_device_channel)

## 用途
物理表 `device.t_device_channel`,主键 `id`。设备渠道。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `merchant_mid` | varchar(50) | 商户mid |
| `device_id` | bigint | 设备ID |
| `mid` | varchar(50) | 二级商户号 |
| `tid` | varchar(50) | 外部设备号 |
| `tpdu` | varchar(50) | The Transaction Protocol Data Unit - EFTLab · 可空 |
| `cvm_limit` | int | cvm limit · 可空 |
| `store_id` | varchar(30) | store id · 可空 |
| `channel_code` | varchar(50) | 渠道编码 |
| `status` | varchar(32) | 状态 ENABLE 可用 DISABLED 已停用 |
| `created_time` | timestamp | 创建时间 |
| `last_updated_time` | timestamp | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `UIDX_MID_TID`:merchant_mid, tid, channel_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
