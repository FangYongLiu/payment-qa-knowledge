---
id: tbl_rdgs_t_dealing_record
object_type: Table
name: 直连渠道换汇充值记录 (t_dealing_record)
aliases: [t_dealing_record, rdgs.t_dealing_record]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: rdgs schema DDL
tags: [payment-core, rdgs]
sensitivity: normal
related_services: []
---

# 直连渠道换汇充值记录 (t_dealing_record)

## 用途
物理表 `rdgs.t_dealing_record`,主键 `record_id`。直连渠道换汇充值记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `record_id` | bigint | 主键ID |
| `channel_code` | varchar(12) | 渠道CODE |
| `country_code` | char(2) | 国家CODE |
| `value_date_type` | char(4) | 汇款类型时效;Cash,TOM,SPOT |
| `from_amount` | decimal(15, 4) | 换汇原金额;换汇时的原金额 |
| `from_currency` | char(3) | 换汇币种;换汇时的币种如USD |
| `to_amount` | decimal(15, 4) | 目标金额;目标金额 |
| `to_currency` | char(3) | 目标币种;目标币种如PKR |
| `local_amount` | decimal(15, 4) | 本币金额;AED金额 |
| `local_currency` | char(3) | 本币种;AED |
| `balance_amount` | decimal(18, 4) | 渠道实时余额 · 可空 |
| `balance_currency` | char(3) | 预存款币种 · 可空 |
| `base_rate` | decimal(15, 8) | 基础汇率;换汇币种与本币汇率(USD:AED)，保留4位小数 |
| `deal_rate` | decimal(15, 8) | 换汇汇率;换汇币种原币种与目标币种汇率(USD:PKR) |
| `cost_rate` | decimal(15, 8) | 陈本汇率;AED:PKR · 可空 |
| `status` | char | 状态;I: Created,V:Valid,C:Cancel |
| `dealing_date` | datetime | 换汇日期;换汇日期YYYYMMDD |
| `value_date` | datetime | 到账日期 · 可空 |
| `finish_time` | timestamp | 完成时间 · 可空 |
| `operator_name` | varchar(64) | 操作员 · 可空 |
| `operator_time` | timestamp | 操作时间 · 可空 |
| `remark` | varchar(255) | 备注;如短信模板需要的变量 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`record_id`
- `idx_create_time`:create_time
- `idx_dealing_date`:dealing_date

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
