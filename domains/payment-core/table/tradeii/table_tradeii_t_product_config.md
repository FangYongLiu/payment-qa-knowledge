---
id: tbl_tradeii_t_product_config
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (tradeii schema) 2026-06-25
tags:
- tradeii
- config
- t_product_config
subdomain: config
module: null
sensitivity: normal
name: 产品配置(t_product_config)
aliases:
- t_product_config
related_services:
- svc_tradeii
related_scenarios: []
---
# 产品配置(t_product_config)

## 用途
产品配置。属 tradeii 库(交易/支付/退款核心),由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](交易核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `config_id` | bigint | PK / AUTO_INC | 配置ID |
| `biz_product_code` | varchar(64) |  | biz productCode |
| `config_code` | varchar(50) | NOT NULL | 配置代码 |
| `config_value` | varchar(255) | NOT NULL | 配置值 |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`config_id`)
- 唯一约束:
  - `uk_biz_key` 唯一 (biz_product_code, config_code)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
