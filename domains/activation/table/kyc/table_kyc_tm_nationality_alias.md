---
id: tbl_kyc_tm_nationality_alias
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
- reference
- tm_nationality_alias
subdomain: reference
module: null
sensitivity: normal
name: 国际名称表(tm_nationality_alias)
aliases:
- tm_nationality_alias
related_services:
- svc_kyc
related_scenarios: []
---

# 国际名称表(tm_nationality_alias)

## 用途
**国籍别名参考表**:国籍编号↔名称↔别名↔alpha3↔国际区号 映射,按通道(channel)。用于把通道返回的国籍归一。参考数据。

## 关联关系
- **所属服务**:[[svc_kyc]](gp078_kyc,= frontmatter `related_services`,tbl→service 边)
- **谁读写它**:由相关 [[api_*]] / [[svc_*]] 的 `related_tables` 声明(impact 分析反向可达,本侧不重复列)。
- **哪些场景校验它**:待补(暂无直接关联场景对象)。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `id` | bigint | PK / NOT NULL | 主键ID |
| `channel` | varchar(50) |  | 通道 |
| `nationality` | int |  | 国籍编号 |
| `nationality_name` | varchar(500) |  | 国籍名称 |
| `nationality_alias` | varchar(2000) |  | 国籍别名 |
| `create_time` | timestamp |  | 创建时间 |
| `update_time` | timestamp |  | 修改时间 |
| `nationality_short_name` | varchar(50) |  | 国籍简称 |
| `short_name_alpha3` | char(3) |  | 国籍3位code |
| `international_telephone_code` | varchar(50) |  | 国际电话编号 |

## 主键 / 索引
- 主键:(`id`)
- 索引:无(除主键外原文未定义)

## 校验点(QA 关注)
- alpha3/区号正确;别名覆盖各通道写法。
- 通道返回国籍能命中本表归一化。
