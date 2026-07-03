---
id: tbl_acquireii_t_pos_settlement
object_type: Table
name: pos结算 (t_pos_settlement)
aliases: [t_pos_settlement, acquireii.t_pos_settlement]
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

# pos结算 (t_pos_settlement)

## 用途
物理表 `acquireii.t_pos_settlement`,主键 `settlement_id`。pos结算。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `settlement_id` | bigint | 结算ID |
| `device_id` | varchar(32) | 发起方设备id |
| `partner_id` | varchar(32) | 发起方memberId |
| `start_time` | timestamp(3) | 开始时间 |
| `end_time` | timestamp(3) | 结束时间 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |
| `operator_id` | varchar(50) | 操作员 |

## 主键 / 索引
- 主键:`settlement_id`
- `uk_ps_device`:device_id (UNIQUE)
- `i_ps_lut`:last_updated_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
