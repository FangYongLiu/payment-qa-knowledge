---
id: tbl_member_tr_member_attachments
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
- member
- tr_member_attachments
subdomain: member
module: null
sensitivity: normal
name: 会员附件表(tr_member_attachments)
aliases:
- tr_member_attachments
related_services:
- svc_member
related_scenarios: []
---

# 会员附件表(tr_member_attachments)

## 用途
会员附件表。属 member 库,由 [[svc_member]] 读写。

## 关联关系
- **所属服务**:[[svc_member]](member 会员/账户核心,= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ATTACH_ID` | varchar(32) | PK / NOT NULL | 附件ID |
| `ATTACH_TYPE` | varchar(32) | NOT NULL | 附件类型 |
| `ATTACH_NAME` | varchar(100) |  | 附件名称 |
| `UFS_PATH` | varchar(500) |  | UFS路径 |
| `STATUS` | char |  | 状态 |
| `UPLOAD_TIME` | timestamp |  | 上传时间 |
| `CREATE_TIME` | timestamp |  | 创建时间 |
| `UPDATE_TIME` | timestamp |  | 修改时间 |
| `MEMO` | varchar(200) |  | 备注 |
| `MEMBER_ID` | varchar(32) |  | 会员ID |
| `BATCH_ID` | varchar(32) |  | 批次ID |

## 主键 / 索引
- 主键:(`ATTACH_ID`)
- 索引:见 DDL(此处省略,可按需补)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
