---
id: tbl_marketnotify_t_market_match_config
object_type: Table
name: 活动匹配 (t_market_match_config)
aliases: [t_market_match_config, marketnotify.t_market_match_config]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: marketnotify schema DDL
tags: [marketing, marketnotify]
sensitivity: normal
related_services: []
---

# 活动匹配 (t_market_match_config)

## 用途
物理表 `marketnotify.t_market_match_config`,主键 `id`。活动匹配。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | ID · 可空 |
| `activity_id` | varchar(32) | 活动id：活动id |
| `job_code` | varchar(32) | 活动job：匹配job |
| `partner_id` | varchar(32) | 平台方id：平台方id · 可空 |
| `kyc_flag` | char | kyc标记：Y,N,为空表示都匹配 · 可空 |
| `exec_type` | char | 处理方式：D=延迟，I=立即 |
| `memo` | varchar(255) | 备注 · 可空 |
| `enable_flag` | char | 启用标识：Y=启用，N=停用 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
