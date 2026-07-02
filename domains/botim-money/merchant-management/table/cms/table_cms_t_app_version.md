---
id: tbl_cms_t_app_version
object_type: Table
name: APP版本 (t_app_version)
aliases: [t_app_version, cms.t_app_version]
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

# APP版本 (t_app_version)

## 用途
物理表 `cms.t_app_version`,主键 `id`。APP版本。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(18) | 主键 · 可空 |
| `version_no` | bigint | 版本号 |
| `version_name` | varchar(120) | 版本名称 |
| `vector_code` | varchar(18) | 载体Id |
| `platform_type` | varchar(18) | 终端类型:ios,android |
| `package_type` | varchar(12) | 包类型：SDK，APP，ALL · 可空 |
| `release_notes` | varchar(500) | 版本说明 · 可空 |
| `download_url` | varchar(255) | 下载地址 · 可空 |
| `download_type` | varchar(16) | 下载的类型 · 可空 |
| `app_channel` | varchar(20) | app渠道 · 可空 |
| `app_size` | varchar(16) | App大小 · 可空 |
| `images` | varchar(150) | 宣传图片地址 · 可空 |
| `is_force` | tinyint(2) | 是否是强制更新:0-非强制更新 1-强制更新 2-推荐更新 · 可空 |
| `is_tip` | tinyint(2) | 是否提示更新:0-不提示 1-提示 · 可空 |
| `status` | tinyint(2) | 是否有效:0-失效，1-有效 · 可空 |
| `not_support_apis` | varchar(2048) | 当前版本不支持的Api · 可空 |
| `user_tags` | varchar(500) | 用户标签组 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
