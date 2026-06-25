---
id: tbl_aml_t_product_code_dic
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_product_code_dic
subdomain: aml
module: null
sensitivity: normal
name: 交易产品码字典表(t_product_code_dic)
aliases:
- t_product_code_dic
related_services:
- svc_aml
related_scenarios: []
---
# 交易产品码字典表(t_product_code_dic)

## 用途
交易产品码字典表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `product_code` | varchar(16) | NOT NULL | code |
| `product_code_desc` | varchar(32) | 默认 '' | code描述 |
| `tmx_code` | varchar(40) |  | 产品码在tmx对应的code |
| `limit_strategy` | varchar(32) | NOT NULL / 默认 'OUT,IN' | 限额限次策略 |
| `pay_channel_limit` | varchar(32) | 默认 '14' | 支付方式限制,如果为空，则所有支付方式全限 |
| `create_time` | timestamp | 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | 默认 CURRENT_TIMESTAMP | 更新时间 |
| `create_by` | varchar(32) |  | 创建者 |
| `update_by` | varchar(32) |  | 更新者 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
