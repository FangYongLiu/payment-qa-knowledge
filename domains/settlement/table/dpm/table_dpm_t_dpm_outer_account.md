---
id: tbl_dpm_t_dpm_outer_account
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
- t_dpm_outer_account
subdomain: dpm
module: null
sensitivity: normal
name: 外部账户(客户分户账)(t_dpm_outer_account)
aliases:
- t_dpm_outer_account
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 外部账户(客户分户账)(t_dpm_outer_account)

## 用途
外部账户(客户分户账)。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ACCOUNT_NO` | varchar(32) | PK / NOT NULL | 账户号 |
| `ACCOUNT_TITLE_NO` | varchar(32) |  | 科目号 |
| `ACCOUNT_NAME` | varchar(128) |  | 账户名称 |
| `OPEN_DATE` | timestamp |  | 开户日期(创建时间) |
| `MEMBER_ID` | varchar(15) |  | 会员号 |
| `STATUS_MAP` | varchar(6) |  | 状态位图(激活/锁定/冻结/销户) |
| `ACCOUNT_ATTRIBUTE` | decimal(1) |  | 账户属性 1:对私 2:对公 |
| `ACCOUNT_TYPE` | decimal(4) |  | 账户类型 1:基本户 2:一般户 3:专用户 4:临时户 5:保证金户 |
| `CURR_BAL_DIRECTION` | decimal(1) |  | 当前余额方向 1:借 2:贷 |
| `BAL_DIRECTION` | decimal(1) |  | 账户余额方向 1:借 2:贷 0:双向 |
| `CURRENCY_CODE` | varchar(3) |  | 货币类型 |
| `accounting_version` | bigint | NOT NULL / 默认 0 | 记账版本 |
| `LAST_UPDATE_TIME` | timestamp |  | 更新时间 |
| `REQUEST_NO` | varchar(32) | NOT NULL | 开外部户请求请求号:不可为空 需唯一 |

## 主键 / 索引
- 主键:(`ACCOUNT_NO`)
- 唯一约束:
  - `UIDX_DOAO_RO` 唯一 (REQUEST_NO)
- 索引:
  - `IDX_OA_MEMBER_ID` (MEMBER_ID)
  - `IDX_T_DPM_OUTER_ACCOUNT` (OPEN_DATE)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
