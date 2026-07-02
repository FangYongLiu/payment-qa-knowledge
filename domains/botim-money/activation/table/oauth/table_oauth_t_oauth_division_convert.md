---
id: tbl_oauth_t_oauth_division_convert
object_type: Table
name: 行政区域转换 (t_oauth_division_convert)
aliases: [t_oauth_division_convert, oauth.t_oauth_division_convert]
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

# 行政区域转换 (t_oauth_division_convert)

## 用途
物理表 `oauth.t_oauth_division_convert`,主键 `id`。行政区域转换。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识 |
| `division_id` | bigint | 区域id。依赖t_oauth_division.id |
| `app_id` | bigint | 三方应用id。依赖t_oauth_client_app.id |
| `app_division_id` | varchar(99) | 三方应用的区域id |
| `division_code` | varchar(99) | 所有上级的编号。例：AS.CN.AH.AQ0.QS0.SH0.010。冗余。t_oauth_client_app.division_code |
| `name` | varchar(99) | 名称。默认中文名。或者本地名字。冗余。 |
| `app_name` | varchar(99) | 三方应用名称。只起备注作用 |
| `create_time` | bigint | 创建时间 |
| `update_time` | bigint | 更新时间 |
| `enable_flag` | varchar(2) | 可用标志。Y可用，或者其它代表“删除” |

## 主键 / 索引
- 主键:`id`
- `i_odc_app_division_id`:app_division_id
- `i_odc_division_id`:division_id

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
