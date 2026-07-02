---
id: tbl_cms_t_user_tag
object_type: Table
name: cms用户标签组 (t_user_tag)
aliases: [t_user_tag, cms.t_user_tag]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cms schema DDL
tags: [merchant-management, cms]
sensitivity: normal
related_services: []
---

# cms用户标签组 (t_user_tag)

## 用途
物理表 `cms.t_user_tag`,主键 `id`。cms用户标签组。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `user_identity` | varchar(36) | 会员标识 |
| `user_key` | varchar(10) | 会员key：phone ,uid ,memberId |
| `tag_code` | varchar(18) | 标签code |
| `tag_name` | varchar(18) | 标签名 |
| `status` | tinyint | 是否有效:0-失效，1-有效 · 可空 |
| `begin_time` | timestamp | 开始时间 |
| `end_time` | timestamp | 结束时间 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_user_identity`:tag_code, user_key, user_identity (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
