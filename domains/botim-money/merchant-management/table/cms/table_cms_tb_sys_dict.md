---
id: tbl_cms_tb_sys_dict
object_type: Table
name: 基础字典 (tb_sys_dict)
aliases: [tb_sys_dict, cms.tb_sys_dict]
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

# 基础字典 (tb_sys_dict)

## 用途
物理表 `cms.tb_sys_dict`,主键 `dict_id`。基础字典。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `dict_id` | bigint | 字典id · 可空 |
| `dict_type_id` | bigint | 所属字典类型的id |
| `code` | varchar(50) | 字典编码 |
| `name` | varchar(255) | 字典名称 |
| `parent_id` | bigint | 上级代码id |
| `parent_ids` | varchar(255) | 所有上级id · 可空 |
| `status` | varchar(10) | 状态（字典） |
| `sort` | tinyint | 排序 · 可空 |
| `description` | varchar(1000) | 字典的描述 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |
| `create_user` | bigint | 创建人 · 可空 |
| `update_user` | bigint | 修改人 · 可空 |

## 主键 / 索引
- 主键:`dict_id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
