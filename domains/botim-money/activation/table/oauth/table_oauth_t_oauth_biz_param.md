---
id: tbl_oauth_t_oauth_biz_param
object_type: Table
name: 业务参数 (t_oauth_biz_param)
aliases: [t_oauth_biz_param, oauth.t_oauth_biz_param]
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

# 业务参数 (t_oauth_biz_param)

## 用途
物理表 `oauth.t_oauth_biz_param`,主键 `id`。业务参数。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | PK系统生成，数据的唯一标识 |
| `classify` | varchar(255) | 参数类型 |
| `bond` | varchar(255) | 参数键 |
| `val` | varchar(10000) | 参数值 |
| `name` | varchar(255) | 参数名 |
| `sort` | bigint | 数据序号 |
| `ext` | varchar(1024) | 扩展信息，用来存放一些扩展的参数 |
| `remark` | varchar(64) | 备注，运维备注 |
| `status` | varchar(64) | 数据的状态，可用来标记数据的临时修改，也可以用来标记数据迁移的状态 |
| `ver` | bigint | 数据版号，更新时以此判断，数据没有被其它人并发修改，从0开始 |
| `create_time` | bigint | 创建时间 |
| `update_time` | bigint | 更新时间 |
| `enable_flag` | varchar(2) | 可用标志。Y可用，或者其它代表“删除” |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
