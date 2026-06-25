---
id: tbl_aml_t_member_attachments
object_type: Table
domain: compliance
status: active
owner: dewen.li
reviewer: dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (aml schema) 2026-06-25
tags:
- aml
- aml
- t_member_attachments
subdomain: aml
module: null
sensitivity: normal
name: Risk会员附件表(t_member_attachments)
aliases:
- t_member_attachments
related_services:
- svc_aml
related_scenarios: []
---
# Risk会员附件表(t_member_attachments)

## 用途
Risk会员附件表。属 aml 库,由 [[svc_aml]] 读写。

## 关联关系
- **所属服务**:[[svc_aml]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | int | PK / AUTO_INC | 附件ID |
| `member_id` | varchar(20) |  | 会员ID |
| `attach_type` | varchar(32) | NOT NULL | 附件类型 |
| `ref_id` | bigint |  | 关联ID |
| `attach_name` | varchar(100) |  | 附件名称 |
| `ufs_path` | varchar(500) |  | UFS路径 |
| `status` | char(2) |  | 状态 |
| `upload_time` | timestamp |  | 上传时间 |
| `create_time` | timestamp |  | 创建时间 |
| `update_time` | timestamp |  | 修改时间 |
| `memo` | varchar(200) |  | 备注 |
| `create_user` | varchar(50) |  | 建立人 |
| `update_user` | varchar(50) |  | 更新人 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `inx_member_id` (member_id)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
