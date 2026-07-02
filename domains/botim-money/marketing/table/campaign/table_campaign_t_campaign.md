---
id: tbl_campaign_t_campaign
object_type: Table
name: t_campaign (t_campaign)
aliases: [t_campaign, campaign.t_campaign]
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

# t_campaign (t_campaign)

## 用途
物理表 `campaign.t_campaign`,主键 `cmpn_id`。(DDL 未提供表注释)。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `cmpn_id` | bigint | 主键 · 可空 |
| `cmpn_cate` | varchar(10) | 活动分类 · 可空 |
| `cmpn_name` | varchar(50) | 活动名称 |
| `show_name` | varchar(50) | 活动展示名称 · 可空 |
| `status` | varchar(10) | 活动状态 待发布:UP  运行中:RUN 活动结束:END |
| `start_time` | timestamp | 活动开始时间 · 可空 |
| `end_time` | timestamp | 活动结束时间 · 可空 |
| `link_url` | varchar(125) | 活动页面地址 · 可空 |
| `platform` | varchar(10) | 平台 · 可空 |
| `cmpn_desc` | varchar(125) | 活动描述 · 可空 |
| `memo` | varchar(50) | 备注 · 可空 |
| `source` | varchar(15) | 活动来源 · 可空 |
| `merchant_id` | varchar(32) | 商户id · 可空 |
| `white_list_key` | varchar(50) | 白名单 · 可空 |
| `user_cate` | varchar(15) | 用户分类 · 可空 |
| `placement` | varchar(20) | 投放渠道:offer none · 可空 |
| `create_time` | timestamp | 创建时间 · 可空 |
| `update_time` | timestamp | 更新时间 · 可空 |

## 主键 / 索引
- 主键:`cmpn_id`
- `idx_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
