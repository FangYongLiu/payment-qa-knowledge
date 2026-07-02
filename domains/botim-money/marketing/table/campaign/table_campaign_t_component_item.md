---
id: tbl_campaign_t_component_item
object_type: Table
name: t_component_item (t_component_item)
aliases: [t_component_item, campaign.t_component_item]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: campaign schema DDL
tags: [marketing, campaign]
sensitivity: normal
related_services: []
---

# t_component_item (t_component_item)

## 用途
物理表 `campaign.t_component_item`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `title` | varchar(50) | 标题 · 可空 |
| `sub_title` | varchar(125) | 子标题 · 可空 |
| `img_url` | varchar(125) | 图片地址 · 可空 |
| `target_url` | varchar(125) | 目标地址 · 可空 |
| `start_time` | timestamp | 开始时间 · 可空 |
| `end_time` | timestamp | 结束时间 · 可空 |
| `status` | tinyint | -1 不可用 0 未生效  1已生效 · 可空 |
| `comp_id` | bigint | 组件id · 可空 |
| `comp_cate` | varchar(30) | 组件类别 · 可空 |
| `display_order` | int | 排序 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
