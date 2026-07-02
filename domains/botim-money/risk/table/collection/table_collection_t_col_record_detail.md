---
id: tbl_collection_t_col_record_detail
object_type: Table
name: 通话明细表 (t_col_record_detail)
aliases: [t_col_record_detail, collection.t_col_record_detail]
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: collection schema DDL
tags: [risk, collection]
sensitivity: normal
related_services: []
---

# 通话明细表 (t_col_record_detail)

## 用途
物理表 `collection.t_col_record_detail`,主键 `id`。通话明细表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主健ID · 可空 |
| `create_by` | varchar(100) | 创建者 · 可空 |
| `update_by` | varchar(100) | 更新者 · 可空 |
| `create_time` | timestamp | 创建日期 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `bill_no` | varchar(64) | 订单 · 可空 |
| `phone` | varchar(50) | 被叫电话 不带区号 · 可空 |
| `status` | smallint(5) | 状态 |
| `type` | tinyint(5) | 类型1:nx 2:3cx · 可空 |
| `file_tag` | varchar(255) | ufs存储tag · 可空 |
| `fail_count` | smallint(5) | 失败次数 · 可空 |
| `user_uid` | varchar(50) | 催收员uid · 可空 |
| `duration` | smallint(5) | 时长 · 可空 |
| `user_name` | varchar(50) | 拨打账户 · 可空 |
| `start_time` | timestamp | 开始时间 · 可空 |
| `end_time` | timestamp | 结束时间 · 可空 |
| `answer_time` | timestamp | 接通时间 · 可空 |
| `effective_called_number` | varchar(50) | 被叫规整后电话 完整被叫电话 · 可空 |
| `hangup_cause` | varchar(255) | 挂断原因 · 可空 |
| `order_id` | varchar(50) | 牛信电话订单号 webphone时为订单号 否则为自动生成 · 可空 |
| `country_code` | varchar(50) | 地区代码 · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_bill_no`:bill_no
- `idx_end_time`:end_time
- `idx_order_id`:order_id
- `idx_phone`:phone
- `idx_start_time`:start_time
- `idx_user_uid`:user_uid
- `inx_phone`:effective_called_number

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
