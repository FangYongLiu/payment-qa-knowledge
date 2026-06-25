---
id: tbl_remittance_t_public_notice
object_type: Table
domain: remittance
status: active
owner: lei.pan
reviewer: lei.pan
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (remittance schema) 2026-06-25
tags:
- remittance
- remittance
- t_public_notice
subdomain: remittance
module: null
sensitivity: normal
name: 公告(t_public_notice)
aliases:
- t_public_notice
related_services:
- svc_remittance
related_scenarios: []
---
# 公告(t_public_notice)

## 用途
公告。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 主键 |
| `channel_code` | varchar(12) | NOT NULL | 渠道编码 |
| `start_time` | timestamp | NOT NULL | 开始时间 |
| `end_time` | timestamp | NOT NULL | 结束时间 |
| `notice_content` | varchar(255) |  | 内容 |
| `icon` | varchar(100) |  | icon |
| `status` | char(2) |  | 状态(Y/N) |
| `create_time` | timestamp | NOT NULL | 更新时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
