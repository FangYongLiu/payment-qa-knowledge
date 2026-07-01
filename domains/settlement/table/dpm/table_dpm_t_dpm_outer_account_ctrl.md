---
id: tbl_dpm_t_dpm_outer_account_ctrl
object_type: Table
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (dpm schema) 2026-06-25
tags:
- dpm
- dpm
- t_dpm_outer_account_ctrl
subdomain: dpm
module: null
sensitivity: normal
name: 外部开户约束表(t_dpm_outer_account_ctrl)
aliases:
- t_dpm_outer_account_ctrl
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 外部开户约束表(t_dpm_outer_account_ctrl)

## 用途
外部开户约束表。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `REQUEST_NO` | varchar(32) | PK / NOT NULL | 开外部户请求请求号:不可为空 需唯一 |
| `MEMBER_ID` | varchar(32) | NOT NULL | 会员ID |
| `CURRENCY` | char(3) | 默认 'AED' | 币种 |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp | NOT NULL | 最后修改时间 |

## 主键 / 索引
- 主键:(`REQUEST_NO`)
- 唯一约束:
  - `UIDX_DOA_RO` 唯一 (MEMBER_ID, CURRENCY)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
