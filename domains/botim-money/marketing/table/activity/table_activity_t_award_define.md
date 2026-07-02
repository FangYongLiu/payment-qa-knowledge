---
id: tbl_activity_t_award_define
object_type: Table
name: 券定义表#记录券定义#新增券定义或要调整券定义内容时要新增或修改记录#yanghuilong (t_award_define)
aliases: [t_award_define, activity.t_award_define]
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

# 券定义表#记录券定义#新增券定义或要调整券定义内容时要新增或修改记录#yanghuilong (t_award_define)

## 用途
物理表 `activity.t_award_define`,主键 `id`。券定义表#记录券定义#新增券定义或要调整券定义内容时要新增或修改记录#yanghuilong。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int(10) | id · 可空 |
| `define_code` | varchar(128) | 优惠券定义code/英文名称 |
| `define_name` | varchar(255) | 优惠券定义描述 · 可空 |
| `award_name` | varchar(64) | 优惠券名称：显示给用户的 · 可空 |
| `award_description` | varchar(255) | 券使用规则描述 · 可空 |
| `award_reduce_way` | smallint(4) | 实施优惠的方式：1、减金额；2、打折 |
| `award_quantity_type` | smallint(4) | 待补 |
| `award_usage_type` | smallint(4) | 优惠券按使用类型分类类型，1：抵扣券；2：满减券；4：循环满减券 |
| `currency` | varchar(16) | 货币类型，如AED · 可空 |
| `condition_amount` | varchar(255) | 待补 |
| `max_deduct_amount` | int(10) | 最多抵扣金额 · 可空 |
| `ast_determine_way` | smallint(4) | 待补 |
| `aet_determine_way` | smallint(4) | 待补 |
| `period` | int (10) | 待补 · 可空 |
| `award_start_time` | timestamp | 待补 · 可空 |
| `award_end_time` | timestamp | 待补 · 可空 |
| `define_start_time` | timestamp | 券定义的有效期开始时间 · 可空 |
| `define_end_time` | timestamp | 券定义的有效期结束时间 · 可空 |
| `status` | smallint(4) | 待补 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `product` | smallint(4) | 1、cashnow，2、paylater，3、wecredit |
| `award_type` | smallint(4) | 1、常规券，系统要负责状态流转。2、纯展示券，系统不负责状态流转 |

## 主键 / 索引
- 主键:`id`
- `ix_name`:define_code (UNIQUE)
- `ix_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
