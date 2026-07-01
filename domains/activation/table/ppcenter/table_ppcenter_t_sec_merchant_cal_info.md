---
id: tbl_ppcenter_t_sec_merchant_cal_info
object_type: Table
domain: activation
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (ppcenter schema) 2026-06-25
tags:
- ppcenter
- pricing
- t_sec_merchant_cal_info
subdomain: pricing
module: null
sensitivity: normal
name: 二级商户算费信息(t_sec_merchant_cal_info)
aliases:
- t_sec_merchant_cal_info
related_services:
- svc_ppcenter
related_scenarios: []
---
# 二级商户算费信息(t_sec_merchant_cal_info)

## 用途
二级商户算费信息。属 ppcenter 库,由 [[svc_ppcenter]] 读写。

## 关联关系
- **所属服务**:[[svc_ppcenter]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 主键id |
| `apply_id` | int |  | 申请id |
| `sec_merchant_fee` | decimal(8,6) |  | 二级商户手续费 |
| `sec_merchant_vat` | decimal(8,6) |  | 二级商户手续费增值税 |
| `rebate` | decimal(8,6) |  | 抽佣比例 |
| `extension` | varchar(255) |  | 扩展参数 |
| `gmt_create` | timestamp | NOT NULL | 创建时间 |
| `gmt_modify` | timestamp | 默认 CURRENT_TIMESTAMP | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
