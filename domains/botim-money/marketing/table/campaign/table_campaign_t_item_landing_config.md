---
id: tbl_campaign_t_item_landing_config
object_type: Table
name: t_item_landing_config (t_item_landing_config)
aliases: [t_item_landing_config, campaign.t_item_landing_config]
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

# t_item_landing_config (t_item_landing_config)

## 用途
物理表 `campaign.t_item_landing_config`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `branch_name` | varchar(50) | 分支名称 · 可空 |
| `offer_name` | varchar(50) | 活动名称 · 可空 |
| `img_url` | varchar(125) | 图片地址 · 可空 |
| `start_time` | timestamp | 开始时间 · 可空 |
| `end_time` | timestamp | 结束时间 · 可空 |
| `offer_detail` | varchar(1000) | offer描述 · 可空 |
| `btn_name` | varchar(50) | 按钮名称 · 可空 |
| `target_url` | varchar(125) | 目标地址 · 可空 |
| `cmpn_id` | bigint | 活动id · 可空 |
| `landing_cate` | varchar(10) | 子页面分类 · 可空 |
| `item_id` | bigint | 布局id · 可空 |
| `create_time` | timestamp | 开始时间 · 可空 |
| `update_time` | timestamp | 结束时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
