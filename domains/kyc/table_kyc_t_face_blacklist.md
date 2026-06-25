---
id: tbl_kyc_t_face_blacklist
object_type: Table
domain: kyc
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-06-24'
source_type: DB DDL
source_ref: DataGrip DDL export (kyc schema) 2026-06-24
tags:
- kyc
- risk
- t_face_blacklist
subdomain: risk
module: null
sensitivity: restricted
name: 人脸黑名单表(t_face_blacklist)
aliases:
- t_face_blacklist
related_services:
- svc_kyc
related_scenarios: []
---

# 人脸黑名单表(t_face_blacklist)

## 用途
**人脸黑名单表**:黑名单人脸(face_tag/特征 feature_id)与来源(member/idn 密文),`status` 失效/生效。活体/比对时拦截。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(32) | PK | 主键 |
| `task_id` | varchar(32) |  | 来源任务ID |
| `member_id` | varchar(20) |  | 来源会员ID |
| `idn` | varchar(50) |  | 来源证件号密文 |
| `mobile` | varchar(50) |  | 手机号（密文和掩码） |
| `face_tag` | varchar(128) | NOT NULL | 人脸图片 |
| `status` | char | NOT NULL | 名单状态（0:失效，1:生效） |
| `operator` | varchar(128) |  | 操作员 |
| `feature_id` | varchar(35) |  | 图片特征ID |
| `memo` | varchar(255) |  | 备注 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_face_tag`:(`face_tag`)

## 校验点(QA 关注)
- 生效名单命中(见 t_face_blacklist_check_record) 应拦截。
- face_tag/feature_id 与比对链路一致;敏感数据访问控制。
