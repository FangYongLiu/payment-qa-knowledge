---
id: tbl_creditues_tb_data_type_config
object_type: Table
name: 数据类型表：数据类型 (tb_data_type_config)
aliases: [tb_data_type_config, creditues.tb_data_type_config]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: creditues schema DDL
tags: [lending, creditues]
sensitivity: normal
related_services: []
---

# 数据类型表：数据类型 (tb_data_type_config)

## 用途
物理表 `creditues.tb_data_type_config`,主键 `id`。数据类型表：数据类型。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | id：ID · 可空 |
| `data_type` | varchar(32) | 数据类型：如mobile_no,email,银行卡，身份证等 · 可空 |
| `validate_type` | varchar(32) | 验证类型：regex,velocity · 可空 |
| `express` | varchar(255) | 表达式：正则或者velocity表达式 · 可空 |
| `enable_flag` | char | 启用标识：Y=启用，N=停用 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `uk_data_type`:data_type (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
