---
id: tbl_casheatm_t_rider
object_type: Table
name: 骑手 (t_rider)
aliases: [t_rider, casheatm.t_rider]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: casheatm schema DDL
tags: [online-business, casheatm]
sensitivity: normal
related_services: [svc_cash_eatm]
---

# 骑手 (t_rider)

## 用途
物理表 `casheatm.t_rider`,主键 `id`。骑手。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `emid` | varchar(200) | 身份证id |
| `name` | varchar(200) | 名字 |
| `mobile_number` | varchar(200) | 手机号明文 · 可空 |
| `totok_uid` | varchar(200) | totok_uid · 可空 |
| `totok_id` | varchar(200) | totok_id · 可空 |
| `device_id` | bigint | 设备id |
| `created_time` | timestamp | 创建时间 |
| `last_updated_time` | timestamp | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `status` | varchar(50) | 待补 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
