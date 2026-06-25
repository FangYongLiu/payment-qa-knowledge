---
id: tbl_member_tm_device
object_type: Table
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (member schema) 2026-06-25
tags:
- member
- device
- tm_device
subdomain: device
module: null
sensitivity: normal
name: 设备信息表(tm_device)
aliases:
- tm_device
related_services:
- svc_member
related_scenarios: []
---

# 设备信息表(tm_device)

## 用途
设备信息表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | int(10) | PK | 主键 |
| `DEVICE_MODEL` | varchar(100) | 默认 '' | 设备型号 |
| `OPER_SYSTEM` | varchar(50) | NOT NULL / 默认 '' | IOS/Android/Other |
| `OPER_SYSTEM_VERSION` | varchar(16) | 默认 '' | 操作系统版本 |
| `SCREEN_RATIO` | varchar(10) | 默认 '' | 屏幕分辨率 |
| `UUID` | varchar(50) | NOT NULL / 默认 '' | uuid |
| `APP_VERSION` | varchar(16) | 默认 '' | 应用版本 |
| `HOST_APP` | varchar(50) |  | SDK宿主 |
| `LAST_CONNECT_TIME` | timestamp |  | 最后连接时间 |
| `CREATE_TIME` | timestamp |  | 创建时间 |
| `MODIFY_TIME` | timestamp |  | 修改时间 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
