---
id: tbl_cms_tb_sys_dict_type
object_type: Table
name: 字典类型表 (tb_sys_dict_type)
aliases: [tb_sys_dict_type, cms.tb_sys_dict_type]
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

# 字典类型表 (tb_sys_dict_type)

## 用途
物理表 `cms.tb_sys_dict_type`,主键 `dict_type_id`。字典类型表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `dict_type_id` | bigint | 字典类型id · 可空 |
| `code` | varchar(255) | 字典类型编码 |
| `name` | varchar(255) | 字典类型名称 |
| `description` | varchar(1000) | 字典描述 · 可空 |
| `system_flag` | char | 是否是系统字典，Y-是，N-否 |
| `status` | varchar(10) | 状态(字典) |
| `sort` | tinyint | 排序 · 可空 |
| `create_time` | timestamp | 添加时间 · 可空 |
| `create_user` | bigint | 创建人 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |
| `update_user` | bigint | 修改人 · 可空 |

## 主键 / 索引
- 主键:`dict_type_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
