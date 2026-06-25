---
id: tbl_dpm_t_dpm_pay_package
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (dpm schema) 2026-06-25
tags:
- dpm
- dpm
- t_dpm_pay_package
subdomain: dpm
module: null
sensitivity: normal
name: 入账包(t_dpm_pay_package)
aliases:
- t_dpm_pay_package
related_services:
- svc_dpm_accounting
related_scenarios: []
---
# 入账包(t_dpm_pay_package)

## 用途
入账包。属 dpm 库,由 [[svc_dpm_accounting]] 读写。

## 关联关系
- **所属服务**:[[svc_dpm_accounting]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `PACKAGE_NO` | varchar(32) | PK / NOT NULL | PACKAGE_NO |
| `APP_ID` | varchar(10) |  | APP_ID |
| `ACCOUNTING_MODEL` | decimal(1) | NOT NULL | 0:自动 1:一个事务内完成 2:逐笔完成 |
| `ASYN` | decimal(1) | NOT NULL | 0:同步 1:异步 |
| `MAC` | varchar(32) |  | MAC |
| `TOTAL_CNT` | decimal(6) |  | TOTAL_CNT |
| `SUCCESS_CNT` | decimal(6) |  | SUCCESS_CNT |
| `FAIL_CNT` | decimal(6) |  | FAIL_CNT |
| `STATUS` | decimal(1) | NOT NULL | 0:初始 1:处理中 2:入账完成(成功) 3:入账失败,处理中 4:入账完成(失败) |
| `ACCOUNTING_DESC` | varchar(128) |  | ACCOUNTING_DESC |
| `RETRY_CNT` | decimal(6) |  | RETRY_CNT |
| `NOTIFY_URL` | varchar(128) |  | NOTIFY_URL |
| `NOTIFY_STATUS` | decimal(1) |  | 0:初始 1:通知成功 2:通知失败 |
| `NOTIFY_DESC` | varchar(64) |  | NOTIFY_DESC |
| `CREATE_TIME` | timestamp |  | CREATE_TIME |
| `LAST_UPDATE_TIME` | timestamp |  | LAST_UPDATE_TIME |
| `REMARK` | varchar(256) |  | 备注 |

## 主键 / 索引
- 主键:(`PACKAGE_NO`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
