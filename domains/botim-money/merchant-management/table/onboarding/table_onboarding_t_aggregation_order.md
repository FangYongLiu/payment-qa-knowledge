---
id: tbl_onboarding_t_aggregation_order
object_type: Table
name: aggregation_order (t_aggregation_order)
aliases: [t_aggregation_order, onboarding.t_aggregation_order]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: onboarding schema DDL
tags: [merchant-management, onboarding]
sensitivity: normal
related_services: []
---

# aggregation_order (t_aggregation_order)

## 用途
物理表 `onboarding.t_aggregation_order`,主键 `id`。aggregation_order。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 8+9 |
| `category` | varchar(50) | category |
| `merchant_mid` | varchar(50) | merchantMid |
| `sub_order_count` | int | subOrderCount · 可空 |
| `status` | varchar(50) | status |
| `fail_code` | varchar(50) | failCode · 可空 |
| `fail_message` | varchar(200) | failMessage · 可空 |
| `created_time` | timestamp(3) | createdTime |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `data_version` | bigint | data_version |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
