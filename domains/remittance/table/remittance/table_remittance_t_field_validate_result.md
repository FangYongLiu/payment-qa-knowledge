---
id: tbl_remittance_t_field_validate_result
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
- t_field_validate_result
subdomain: remittance
module: null
sensitivity: normal
name: 字段验证结果(t_field_validate_result)
aliases:
- t_field_validate_result
related_services:
- svc_remittance
related_scenarios: []
---
# 字段验证结果(t_field_validate_result)

## 用途
字段验证结果。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键，前8后9 |
| `reference_no` | varchar(64) |  | reference no: UPI+id |
| `to_country_code` | char(2) |  | 目标国家 |
| `to_currency_code` | char(3) |  | 目标币种 |
| `transaction_mode` | varchar(16) |  | 汇款模式 |
| `field_code` | varchar(32) |  | 字段code |
| `mapping_code` | varchar(32) |  | 映射实体类的匹配code |
| `field_value` | varchar(100) |  | 用户输入的值 |
| `effect_time` | timestamp |  | 生效时间 |
| `effect_days` | int |  | 有效天数,-1为永久有效 |
| `validate_result` | varchar(255) |  | 验证结果详情JSON |
| `status` | char | NOT NULL | 状态: P=处理中，S=成功，F=失败 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `idx_reference_no` (reference_no)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
