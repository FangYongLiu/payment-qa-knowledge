---
id: tbl_kyc_t_member_kyc_channel
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
- channel
- t_member_kyc_channel
subdomain: channel
module: null
sensitivity: normal
name: 会员实名渠道(t_member_kyc_channel)
aliases:
- t_member_kyc_channel
related_services:
- svc_kyc
related_scenarios: []
---

# 会员实名渠道(t_member_kyc_channel)

## 用途
**会员实名渠道表**:会员可走的实名渠道(`channel_code`:ALL / UAEPASS)。决定该会员走哪条 KYC 通道。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(11) | PK |  |
| `member_id` | varchar(20) | NOT NULL | 会员号 |
| `channel_code` | varchar(10) | NOT NULL | 渠道编码 ALL,UAEPASS |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_tmkc_member_id`:(`member_id`)

## 校验点(QA 关注)
- channel_code 合法值(ALL/UAEPASS);一个会员的渠道唯一性。
- 渠道与 flow_type/通道路由一致。
