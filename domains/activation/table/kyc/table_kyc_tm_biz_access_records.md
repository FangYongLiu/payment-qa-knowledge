---
id: tbl_kyc_tm_biz_access_records
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
- biz-record
- tm_biz_access_records
subdomain: biz-record
module: null
sensitivity: restricted
name: 业务接入记录表(tm_biz_access_records)
aliases:
- tm_biz_access_records
related_services:
- svc_kyc
related_scenarios: []
---

# 业务接入记录表(tm_biz_access_records)

## 用途
**业务接入记录表**:各业务(远程 OCR/EID 验证/活体)的接入流水与状态(含风控拦截=3、超时作废=09)。`biz_body` 存业务数据。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键 |
| `member_id` | varchar(100) |  | 会员ID |
| `access_channel` | varchar(20) |  | 接入平台 |
| `biz_type` | varchar(32) | NOT NULL | 0-远程ORC，1-EID验证，2-活体验证等业务 |
| `biz_body` | varchar(2000) |  | 业务数据 |
| `status` | varchar(4) | NOT NULL | 0-初始化，1-处理成功，2-处理失败，3-风控拦截，4-撤销，5-处理中，09-超时作废 |
| `update_time` | timestamp |  | 更新时间 |
| `create_time` | timestamp |  | 建立时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_tm_biz_access_records_memberid`:(`member_id`)

## 校验点(QA 关注)
- `status` 全状态机(0~5,09)流转;风控拦截(3) 联动 dependency。
- biz_type 与实际业务对应;biz_body 长度上限。
