---
id: tbl_benefit_t_group_config
object_type: Table
name: t_group_config (t_group_config)
aliases: [t_group_config, benefit.t_group_config]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: benefit schema DDL
tags: [marketing, benefit]
sensitivity: normal
related_services: []
---

# t_group_config (t_group_config)

## 用途
物理表 `benefit.t_group_config`,主键 `group_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `group_id` | bigint | 分组id自增 · 可空 |
| `group_code` | varchar(50) | 分组代码 · 可空 |
| `rate_buff` | decimal(10, 4) | 收益率加成 |
| `shares_limit_buff` | decimal(19, 4) | 份额上限加成 |
| `memo` | varchar(255) | 备注信息 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 修改时间 · 可空 |

## 主键 / 索引
- 主键:`group_id`
- `idx_group_code`:group_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
