---
id: tbl_mss_t_algorithm_define
object_type: Table
name: 金额算法【暂无】 (t_algorithm_define)
aliases: [t_algorithm_define, mss.t_algorithm_define]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mss schema DDL
tags: [online-business, mss]
sensitivity: normal
related_services: []
---

# 金额算法【暂无】 (t_algorithm_define)

## 用途
物理表 `mss.t_algorithm_define`,主键 `id`。金额算法【暂无】。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 主键id · 可空 |
| `alg_code` | varchar(32) | 算法code |
| `alg_name` | varchar(64) | 算法名称 |
| `remark` | varchar(32) | 描述 · 可空 |
| `created_time` | timestamp | 创建时间 |
| `updated_time` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
