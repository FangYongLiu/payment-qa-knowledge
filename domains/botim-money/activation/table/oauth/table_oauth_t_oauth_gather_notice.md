---
id: tbl_oauth_t_oauth_gather_notice
object_type: Table
name: 收集通知 (t_oauth_gather_notice)
aliases: [t_oauth_gather_notice, oauth.t_oauth_gather_notice]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: oauth schema DDL
tags: [activation, oauth]
sensitivity: normal
related_services: []
---

# 收集通知 (t_oauth_gather_notice)

## 用途
物理表 `oauth.t_oauth_gather_notice`,主键 `id`。收集通知。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识 |
| `client_app_id` | bigint | 三方应用标识 |
| `gather_classify` | varchar(64) | 收集分类。分全局收货地址gsa，用户收货地址usa |
| `scan_original` | varchar(64) | 数据入口。分t_oauth_access_token，将来的用户表。当gather_classify为gsa时使用 |
| `newest_sign` | varchar(64) | 当前完成的最新的数据的id |
| `scan_leng` | int(4) | 默认50 |
| `notice_data` | varchar(2000) | 要通知的数据的json体 |
| `uid` | varchar(64) | 用户标识。即memberId |
| `data_id` | varchar(64) | 当gather_classify为gsa时为t_oauth_biz_param的id，当gather_classify为usa时，为收货地址的id，仅用于跟踪数据。 |
| `as_finish` | varchar(64) | 已完成为Y，未完成为N。 |
| `create_time` | bigint | 创建时间 |
| `update_time` | bigint | 更新时间 |
| `status` | varchar(64) | 状态 |
| `enable_flag` | varchar(2) | 可用标志。Y可用，N或者其它代表“删除” |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
