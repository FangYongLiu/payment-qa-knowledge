---
id: tbl_remittance_t_channel_return_code
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
- t_channel_return_code
subdomain: remittance
module: null
sensitivity: normal
name: 渠道返回码(t_channel_return_code)
aliases:
- t_channel_return_code
related_services:
- svc_remittance
related_scenarios: []
---
# 渠道返回码(t_channel_return_code)

## 用途
渠道返回码。属 remittance 库,由 [[svc_remittance]] 读写。

## 关联关系
- **所属服务**:[[svc_remittance]](= `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 反向可达)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / AUTO_INC | 配置id |
| `channel_code` | varchar(10) | NOT NULL | 渠道编码 |
| `channel_return_code` | varchar(20) | NOT NULL | 渠道返回码 |
| `channel_return_msg` | varchar(255) |  | 渠道返回信息 |
| `enable_flag` | char | NOT NULL | 启用标识: Y=启用，N=停用 |
| `memo` | varchar(100) |  | 备注 |
| `extension` | varchar(255) |  | 扩展参数 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 修改时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:
  - `uk_channel_code_return_code` (channel_code, channel_return_code)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
