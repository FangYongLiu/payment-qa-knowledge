---
id: tbl_cms_t_page
object_type: Table
name: 页面表 (t_page)
aliases: [t_page, cms.t_page]
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

# 页面表 (t_page)

## 用途
物理表 `cms.t_page`,主键 `page_code`。页面表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `page_code` | bigint(18) | 页面code |
| `project_code` | bigint(18) | 方案code |
| `title_lang_key` | varchar(120) | 标题国际化key:${page}_${section}_${item} · 可空 |
| `user_tag` | varchar(20) | 用户标签 · 可空 |
| `sort_index` | bigint(8) | 排序索引 |
| `icon` | varchar(500) | icon地址 |
| `file_id` | varchar(120) | 文件唯一标识 · 可空 |
| `target_url` | varchar(150) | 跳转路径 · 可空 |
| `description` | varchar(500) | 描述 · 可空 |
| `ext_param` | varchar(500) | 额外参数 · 可空 |
| `config_param` | varchar(500) | 配置参数json格式 · 可空 |
| `gmt_created` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `status` | tinyint | 状态:1-上架 0-下架 · 可空 |
| `version_no` | bigint | 版本号 · 可空 |

## 主键 / 索引
- 主键:`page_code`
- `t_page_uk_page_tittleKey`:page_code, title_lang_key (UNIQUE)
- `t_page_idk`:project_code, page_code

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
