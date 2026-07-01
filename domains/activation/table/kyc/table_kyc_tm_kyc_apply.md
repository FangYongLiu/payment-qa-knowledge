---
id: tbl_kyc_tm_kyc_apply
object_type: Table
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: DB DDL
source_ref: DataGrip DDL export (kyc schema) 2026-06-24
tags:
- kyc
- core
- tm_kyc_apply
subdomain: core
module: null
sensitivity: restricted
name: kyc流程记录表(tm_kyc_apply)
aliases:
- tm_kyc_apply
related_services:
- svc_kyc
related_scenarios:
- scn_kyc_eid_full_journey
- scn_kyc_status_inquire
---

# kyc流程记录表(tm_kyc_apply)

## 用途
KYC 流程**主单**表:一条记录 = 一次实名申请(journey)。`token` 串起整条 journey,`apply_type` 区分 EID/Passport/续期/换绑,`status`+`current_status`(PROCESS→FINISH) 表征流程状态,`flow_type`(OLD/SIGNZY_FULL) 决定走哪条通道。各业务子记录经 `tm_biz_record` 以 `apply_id` 回挂本表。是 start-journey/get-result 等接口的核心读写表。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:[[scn_kyc_eid_full_journey]]、[[scn_kyc_status_inquire]](= `related_scenarios`)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `member_id` | varchar(32) |  | 会员ID |
| `partner_id` | varchar(32) |  | 平台ID |
| `relation_mid` | varchar(32) |  | 关联的memberId |
| `apply_type` | varchar(32) |  | 流程类型 |
| `token` | varchar(32) |  | kyc流程token |
| `step` | varchar(32) |  | 当前步骤 |
| `status` | int |  | 本次kyc流程的状态 |
| `biz_type` | varchar(20) |  | 业务类型 |
| `biz_data` | varchar(255) |  | 业务数据json |
| `flow_type` | varchar(35) |  | Flow Type, eg: OLD, SIGNZY_FULL |
| `current_status` | varchar(25) |  | Current Status, eg: PROCESS, FINISH |
| `journey_flag` | tinyint(2) |  | Journey Flag, eg: 1 |
| `result_msg` | varchar(255) |  | Result Msg |
| `channel` | varchar(75) |  | Channel |
| `success_time` | timestamp |  | Kyc Success Time |
| `retake_times` | tinyint(2) |  | Retake times, eg: 1 |
| `create_time` | timestamp |  | 创建时间 |
| `updated_time` | timestamp |  | 更新时间 |
| `extension` | varchar(255) |  | 扩展字段 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_create_time`:(`create_time`)
- 索引 `idx_kyc_apply_mid`:(`member_id`)
- 索引 `idx_member_apply_ctime`:(`member_id`, `apply_type`, `create_time`)
- 索引 `idx_token`:(`token`)

## 校验点(QA 关注)
- `token` 全局唯一,且与各 `tr_biz_record_*.req_token` 一致(同一 flow id 贯穿全程)。
- `status` 与 `current_status` 流转一致:成功时 current_status=FINISH 且 `success_time` 写入。
- `flow_type` 决定走 signzy 全托管(SIGNZY_FULL) 还是旧通道(OLD),据此校验后续子表落点。
- `retake_times` 重拍计数随 retake-selfie 递增;`apply_type` 与场景(EID/护照/续期)匹配。
