---
id: tbl_tradeii_t_product_account_config
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
- trade
- t_product_account_config
subdomain: trade
module: null
sensitivity: normal
name: 产品账户配置(t_product_account_config)
aliases:
- t_product_account_config
related_services:
- svc_tradeii
related_scenarios: []
---
# 产品账户配置(t_product_account_config)

## 用途
产品账户配置。属 tradeii 库,由 [[svc_tradeii]] 读写。

## 关联关系
- **所属服务**:[[svc_tradeii]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `config_id` | bigint | PK / AUTO_INC | 配置id |
| `biz_product_code` | varchar(10) | NOT NULL | 业务产品码 |
| `rule_type` | varchar(20) | NOT NULL | 规则类型：TRANSFER=过渡户（角色:账户类型），PAY_FEE=付款收费（币种:账号），SETTLE_FEE=结算收费（币种:账号） |
| `rule_config` | varchar(128) | NOT NULL | 规则配置 |
| `is_enabled` | char | NOT NULL | 启用标识：Y=启用，N=停用 |
| `extension` | varchar(255) |  | 扩展参数 |
| `create_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 创建时间 |
| `update_time` | timestamp | NOT NULL / 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`config_id`)
- 唯一约束:
  - `uk_biz_key` 唯一 (biz_product_code, rule_type)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
