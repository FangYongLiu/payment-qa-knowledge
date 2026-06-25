---
id: tbl_kyc_t_eid_fraudlist
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
- t_eid_fraudlist
subdomain: risk
module: null
sensitivity: restricted
name: eid欺诈名单(t_eid_fraudlist)
aliases:
- t_eid_fraudlist
related_services:
- svc_kyc
related_scenarios: []
---

# eid欺诈名单(t_eid_fraudlist)

## 用途
**EID 欺诈名单**:命中欺诈的 EID(密文)名单,`status` 标失效/生效。实名时比对拦截。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint(32) | PK | 主键 |
| `task_id` | varchar(32) |  | 任务ID |
| `member_id` | varchar(20) | NOT NULL | 会员ID |
| `mobile` | varchar(55) |  | 手机号（密文+掩码） |
| `idn` | varchar(55) | NOT NULL | eid密文 |
| `status` | char | NOT NULL | 状态（0:失效，1：生效） |
| `operator` | varchar(50) |  | 操作员 |
| `memo` | varchar(255) |  | 备注 |
| `create_time` | timestamp | NOT NULL | 创建时间 |
| `update_time` | timestamp | NOT NULL | 更新时间 |

## 主键 / 索引
- 主键:(`id`)
- 索引 `idx_idn`:(`idn`)

## 校验点(QA 关注)
- `idn` 密文;生效名单(status=1) 命中应拦截实名。
- 失效(status=0) 不应拦截;operator 操作留痕。
