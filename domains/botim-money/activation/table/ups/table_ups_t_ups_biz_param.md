---
id: tbl_ups_t_ups_biz_param
object_type: Table
name: 业务参数 (t_ups_biz_param)
aliases: [t_ups_biz_param, ups.t_ups_biz_param]
domain: activation
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: ups schema DDL
tags: [activation, ups]
sensitivity: normal
related_services: []
---

# 业务参数 (t_ups_biz_param)

## 用途
物理表 `ups.t_ups_biz_param`,主键 `id`。业务参数。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识 |
| `classify` | varchar(128) | 参数类型 |
| `bond` | varchar(128) | 参数键 |
| `val` | varchar(2000) | 参数值 |
| `name` | varchar(32) | 名称 |
| `ordinal` | bigint | 数据序号 |
| `create_time` | bigint | 创建时间 |
| `modify_time` | bigint | 修改时间 |
| `enable_flag` | varchar(2) | 记录是否有效(未作废),Y有效，N为已作废 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
