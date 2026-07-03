---
id: tbl_jollychic_t_address
object_type: Table
name: 地址 (t_address)
aliases: [t_address, jollychic.t_address]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: jollychic schema DDL
tags: [online-business, jollychic]
sensitivity: normal
related_services: [svc_jollychic_service]
---

# 地址 (t_address)

## 用途
物理表 `jollychic.t_address`,主键 `id`。地址。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | int | 地址id · 可空 |
| `name` | varchar(32) | 姓名 |
| `phoneNo` | varchar(32) | 手机号码 |
| `country` | varchar(32) | 国家 · 可空 |
| `address` | varchar(3072) | 地址 |
| `enable_flag` | char | 启用标识：Y=启用，N=停用 |
| `extension` | varchar(255) | 扩展参数 · 可空 |
| `memo` | varchar(255) | 备注 · 可空 |
| `create_time` | timestamp | 创建时间 |
| `update_time` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
