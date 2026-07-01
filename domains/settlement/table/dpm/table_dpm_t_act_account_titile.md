---
id: tbl_dpm_t_act_account_titile
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
- t_act_account_titile
subdomain: dpm
module: null
sensitivity: normal
name: 会计科目表(t_act_account_titile)
aliases:
- t_act_account_titile
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 会计科目表(t_act_account_titile)

## 用途
会计科目表。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `TITLE_SEQ_NO` | bigint | PK / AUTO_INC | 科目序号 |
| `TITLE_CODE` | varchar(16) | NOT NULL | 科目代码 |
| `TITLE_NAME` | varchar(128) | NOT NULL | 科目名称 |
| `TITLE_LEVEL` | decimal(2) |  | 科目级别 |
| `PARENT_TITLE_CODE` | varchar(16) |  | 父科目 |
| `CURRENCY` | char(3) |  | 币种 |
| `IS_LEAF` | char |  | Y: 是 N: 否 |
| `TYPE` | char | NOT NULL | 类型：1（资产类）；2（负债类）；3(所有者权益)；4（共同类）5(损益类) |
| `BALANCE_DIRECTION` | decimal(1) | NOT NULL | 余额方向 1:借 2:贷 0:双向 |
| `STATUS` | char | NOT NULL | 状态：Y（有效）；N（无效） |
| `tag` | varchar(16) |  | tag |
| `GMT_CREATE` | timestamp | NOT NULL | 创建时间 |
| `GMT_MODIFIED` | timestamp | NOT NULL | 最后修改时间 |
| `MEMO` | varchar(128) |  | 备注 |
| `TITLE_RANGE` | decimal(1) | NOT NULL | 1.内部科目;2,外部科目 |

## 主键 / 索引
- 主键:(`TITLE_SEQ_NO`)
- 唯一约束:
  - `AK_KEY_TITLE_CODE` 唯一 (TITLE_CODE)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
