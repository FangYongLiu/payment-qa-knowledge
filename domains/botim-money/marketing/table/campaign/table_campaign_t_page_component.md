---
id: tbl_campaign_t_page_component
object_type: Table
name: t_page_component (t_page_component)
aliases: [t_page_component, campaign.t_page_component]
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

# t_page_component (t_page_component)

## 用途
物理表 `campaign.t_page_component`,主键 `id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `comp_cate` | varchar(15) | 组件分类 · 可空 |
| `comp_title` | varchar(50) | 组件标题 · 可空 |
| `icon_url` | varchar(125) | 图标地址 · 可空 |
| `show_flag` | tinyint | 是否展示 1 展示 0 不展示 · 可空 |
| `display_order` | int(10) | 展示顺序 · 可空 |
| `version` | varchar(10) | 版本号 · 可空 |
| `btn_img` | varchar(125) | 按钮图片 · 可空 |
| `btn_url` | varchar(125) | 按钮地址 · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
