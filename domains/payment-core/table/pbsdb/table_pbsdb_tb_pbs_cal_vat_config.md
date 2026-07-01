---
id: tbl_pbsdb_tb_pbs_cal_vat_config
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (pbsdb schema) 2026-06-25
tags:
- pbsdb
- pricing
- tb_pbs_cal_vat_config
subdomain: pricing
module: null
sensitivity: normal
name: VAT 算费配置(tb_pbs_cal_vat_config)
aliases:
- tb_pbs_cal_vat_config
related_services:
- svc_pbs
related_scenarios: []
---
# VAT 算费配置(tb_pbs_cal_vat_config)

## 用途
VAT 算费配置。属 pbsdb 库,由 [[svc_pbs]] 读写。

## 关联关系
- **所属服务**:[[svc_pbs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC |  |
| `product_code` | varchar(32) | NOT NULL | product code |
| `channel_mode` | varchar(12) |  | pay channel |
| `party_role` | varchar(10) |  | role |
| `ext_params` | varchar(255) |  | extension |
| `gmt_create` | timestamp | NOT NULL | create time |
| `gmt_modified` | timestamp | NOT NULL | update time |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
