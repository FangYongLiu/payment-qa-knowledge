---
id: tbl_activity_t_award_record
object_type: Table
name: 券记录表#记录发放了的优惠券#发放优惠券或使用优惠券时要新增或修改记录#yanghuilong (t_award_record)
aliases: [t_award_record, activity.t_award_record]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: activity schema DDL
tags: [marketing, activity]
sensitivity: normal
related_services: []
---

# 券记录表#记录发放了的优惠券#发放优惠券或使用优惠券时要新增或修改记录#yanghuilong (t_award_record)

## 用途
物理表 `activity.t_award_record`,主键 `id`。券记录表#记录发放了的优惠券#发放优惠券或使用优惠券时要新增或修改记录#yanghuilong。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id · 可空 |
| `member_id` | bigint(32) | 待补 |
| `award_name` | varchar(64) | 优惠券名称，用于显示给用户 · 可空 |
| `award_description` | varchar(255) | 优惠券使用规则 · 可空 |
| `award_reduce_way` | smallint(4) | 待补 |
| `award_usage_type` | smallint(4) | 待补 |
| `max_deduct_amount` | int | 待补 · 可空 |
| `valid_start_time` | timestamp | 有效期开始日期 · 可空 |
| `valid_end_time` | timestamp | 有效期结束日期 · 可空 |
| `condition_amount` | varchar(255) | 待补 · 可空 |
| `currency` | varchar(16) | 币种类型 |
| `use_business_scene_codes` | varchar(255) | 券的使用场景,多个场景码之间以逗号分隔 · 可空 |
| `award_define_id` | int | 券定义id |
| `status` | smallint(4) | 状态含义：1待使用，2：使用前锁定，3.已使用，4取消使用锁定。 · 可空 |
| `order_id` | varchar(128) | 使用此券的业务端id · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `product` | smallint(4) | 1、cashnow，2、paylater，3、wecredit |
| `award_type` | smallint(4) | 1、常规券，系统要负责状态流转。2、纯展示券，系统不负责状态流转 |

## 主键 / 索引
- 主键:`id`
- `ix_adf`:award_define_id
- `ix_create_time`:create_time
- `ix_member`:member_id
- `ix_valid_end_time`:valid_end_time
- `ix_valid_start_time`:valid_start_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
