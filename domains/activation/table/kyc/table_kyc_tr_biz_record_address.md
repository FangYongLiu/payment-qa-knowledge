---
id: tbl_kyc_tr_biz_record_address
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
- eid
- tr_biz_record_address
subdomain: eid
module: null
sensitivity: restricted
name: 会员eid地址表(tr_biz_record_address)
aliases:
- tr_biz_record_address
related_services:
- svc_kyc
related_scenarios: []
---

# 会员eid地址表(tr_biz_record_address)

## 用途
EID **地址信息表**:实名采集的居住地址(公寓/街道/城市/国家/经纬度等)。`record_id`/`req_token` 关联主流程。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(30) | PK / NOT NULL | 主键 |
| `record_id` | bigint(30) |  | 关联记录ID |
| `req_token` | varchar(32) |  | token |
| `flat_no` | varchar(55) |  | 公寓编号 |
| `building` | varchar(155) |  | 建筑 |
| `street` | varchar(255) |  | 街道 |
| `area` | varchar(55) |  | 区域 |
| `city` | varchar(55) |  | 城市 |
| `province` | varchar(55) |  | 省份（洲） |
| `country` | varchar(55) |  | 国家 |
| `post_code` | varchar(15) |  | 邮政编号 |
| `longitude` | varchar(32) |  | 经度 |
| `latitude` | varchar(32) |  | 维度 |
| `alias` | varchar(100) |  | 地址别名 |
| `memo` | varchar(255) |  | 备注 |
| `create_time` | timestamp |  | 创建时间 |
| `update_time` | timestamp |  | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(除主键外原文未定义)

## 校验点(QA 关注)
- 地址字段完整性;经纬度可空。
- 与会员档案地址的一致性(若下游同步)。
