---
id: tbl_basis_tb_export_template
object_type: Table
name: tb_export_template (tb_export_template)
aliases: [tb_export_template, basis.tb_export_template]
domain: merchant-management
status: active
owner: yijian.tan
reviewer: yijian.tan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: basis schema DDL
tags: [merchant-management, basis]
sensitivity: normal
related_services: []
---

# tb_export_template (tb_export_template)

## 用途
物理表 `basis.tb_export_template`,主键 `template_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `template_id` | bigint | 模板ID · 可空 |
| `identifier` | varchar(128) | 标识符 |
| `script` | varchar(10000) | velocity脚本 |
| `memo` | varchar(128) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`template_id`
- `uk_identifier`:identifier (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
