---
id: tbl_oauth_t_oauth_division
object_type: Table
name: 行政区域 (t_oauth_division)
aliases: [t_oauth_division, oauth.t_oauth_division]
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

# 行政区域 (t_oauth_division)

## 用途
物理表 `oauth.t_oauth_division`,主键 `id`。行政区域。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识 |
| `pid` | bigint | 上级id · 可空 |
| `division_code` | varchar(99) | 所有上级的编号。例：AS.CN.AH.AQ0.QS0.SH0.010。冗余。t_oauth_client_app.division_code |
| `layer` | int(2) | 级别。 |
| `name` | varchar(99) | 名称。默认中文名。或者本地名字 |
| `old_name` | varchar(128) | 曾用名。旧名 |
| `cn_name` | varchar(128) | 英文名。一般用于辅助配置人员或者辅助查找。一般不显示在页面。 |
| `status` | varchar(64) | 状态 |
| `create_time` | bigint | 创建时间 |
| `update_time` | bigint | 更新时间 |
| `enable_flag` | varchar(2) | 可用标志。Y可用，或者其它代表“删除” |

## 主键 / 索引
- 主键:`id`
- `i_od_member_id`:division_code
- `i_od_name`:name

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
