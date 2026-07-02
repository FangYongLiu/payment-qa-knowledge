---
id: tbl_basismcht_tb_dc_insert_code
object_type: Table
name: 自动生成insert代码配置 (tb_dc_insert_code)
aliases: [tb_dc_insert_code, basismcht.tb_dc_insert_code]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basismcht schema DDL
tags: [merchant-management, basismcht]
sensitivity: normal
related_services: []
---

# 自动生成insert代码配置 (tb_dc_insert_code)

## 用途
物理表 `basismcht.tb_dc_insert_code`,主键 `code_id`。自动生成insert代码配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `code_id` | varchar(128) | 代码标识符，一般设为类名 |
| `code` | varchar(10000) | Velocity生成的insert语句代码 |

## 主键 / 索引
- 主键:`code_id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
