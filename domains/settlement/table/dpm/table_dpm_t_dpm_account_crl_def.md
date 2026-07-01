---
id: tbl_dpm_t_dpm_account_crl_def
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
- t_dpm_account_crl_def
subdomain: dpm
module: null
sensitivity: normal
name: 账户类型定义(t_dpm_account_crl_def)
aliases:
- t_dpm_account_crl_def
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 账户类型定义(t_dpm_account_crl_def)

## 用途
账户类型定义。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ACCOUNT_TYPE_ID` | bigint | PK / AUTO_INC | 账户类型ID |
| `ACCOUNT_TITLE_ID` | varchar(32) |  | 账户科目ID |
| `ACCOUNT_ATTRIBUTE` | decimal(1) |  | 1:对私 2:对公 9:内部 |
| `FUND_ATTRIBUTE` | decimal(1) |  | 1:借记 2:贷记/混合 |
| `ACCOUNT_TYPE` | decimal(4) |  | 1:基本户 2:一般户 3:专用户 4:临时户 5:保证金户 |
| `CURRENCY_CODE` | varchar(3) |  | 币种 |
| `BAL_DIRECTION` | decimal(1) |  | 1:借 2:贷 0:双向 |
| `STATUS` | decimal(1) |  | 0:有效 1:无效 |
| `REMARK` | varchar(200) |  | 备注 |
| `INPUT_UID` | varchar(32) |  | 录入人 |
| `INPUT_TIME` | timestamp |  | 录入时间 |
| `CHECK_UID` | varchar(32) |  | 检查人 |
| `CHECK_TIME` | timestamp |  | 检查时间 |

## 主键 / 索引
- 主键:(`ACCOUNT_TYPE_ID`)
- 索引:
  - `AK_KEY_ACCOUNT_TYPE` (ACCOUNT_ATTRIBUTE, ACCOUNT_TYPE)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
