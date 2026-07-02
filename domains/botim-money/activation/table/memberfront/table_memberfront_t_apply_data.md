---
id: tbl_memberfront_t_apply_data
object_type: Table
name: 申请数据表 (t_apply_data)
aliases: [t_apply_data, memberfront.t_apply_data]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: memberfront schema DDL
tags: [activation, memberfront]
sensitivity: normal
related_services: []
---

# 申请数据表 (t_apply_data)

## 用途
物理表 `memberfront.t_apply_data`,主键 `id`。申请数据表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint(32) | 主键 |
| `apply_id` | bigint(32) | applyId |
| `data_code` | varchar(32) | 数据code |
| `data_title` | varchar(150) | 展示标题 · 可空 |
| `data_value` | varchar(500) | 值 |
| `data_type` | varchar(20) | 数据类型（txt - 文本，image - 图片） |
| `data_order` | int | 排序 |
| `memo` | varchar(300) | 备注 · 可空 |
| `extension` | varchar(1000) | json 扩展参数 · 可空 |
| `create_time` | timestamp | 建立时间 |
| `update_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- `t_apply_data_apply_id_index`:apply_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
