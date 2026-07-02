---
id: tbl_mss_t_sign_up_event_log
object_type: Table
name: 报名接口记录 (t_sign_up_event_log)
aliases: [t_sign_up_event_log, mss.t_sign_up_event_log]
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

# 报名接口记录 (t_sign_up_event_log)

## 用途
物理表 `mss.t_sign_up_event_log`,主键 `id`。报名接口记录。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 主键 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 更新时间 |
| `error_message` | varchar(128) | 错误消息 · 可空 |
| `ok` | tinyint | 是否成功 · 可空 |
| `resp_code` | smallint | 返回码 · 可空 |
| `event_id` | varchar(64) | 事件id · 可空 |
| `member_id` | varchar(64) | 用户id · 可空 |
| `merchant_id` | varchar(64) | 商户id · 可空 |
| `pay_channel` | varchar(64) | 支付通道 · 可空 |
| `pay_scence` | varchar(64) | 支付场景 · 可空 |
| `product_code` | varchar(64) | 产品code · 可空 |

## 主键 / 索引
- 主键:`id`
- `idx_sulog_create_time`:create_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
