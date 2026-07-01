---
id: tbl_remittance_t_channel_field_config
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_channel_field_config
subdomain: remittance
module: null
sensitivity: normal
name: 渠道参数配置(t_channel_field_config)
aliases:
- t_channel_field_config
related_services:
- svc_remittance
related_scenarios: []
---
# 渠道参数配置(t_channel_field_config)

## 用途
渠道参数配置。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键 |
| `channel_code` | varchar(16) | NOT NULL | 渠道code |
| `transaction_mode` | varchar(20) | NOT NULL | 汇款模式 |
| `channel_field_code` | varchar(100) |  | 渠道参数code |
| `channel_field_label` | varchar(100) |  | 渠道字段标签 |
| `mapping_field_code` | varchar(100) |  | 映射领域对象属性 |
| `domain_code` | varchar(32) |  | 领域对象 |
| `country_code` | char(2) |  | 2位国家code |
| `currency` | char(3) |  | 币种 |
| `convert_flag` | char |  | 转换标记(Y/N) |
| `enable_flag` | char | NOT NULL | 是否可用（Y/N） |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
