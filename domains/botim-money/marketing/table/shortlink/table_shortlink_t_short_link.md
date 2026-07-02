---
id: tbl_shortlink_t_short_link
object_type: Table
name: 退款订单 (t_short_link)
aliases: [t_short_link, shortlink.t_short_link]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: shortlink schema DDL
tags: [marketing, shortlink]
sensitivity: normal
related_services: []
---

# 退款订单 (t_short_link)

## 用途
物理表 `shortlink.t_short_link`,主键 `id`。退款订单。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id · 可空 |
| `code` | varchar(64) | 短链接码 |
| `url` | varchar(256) | 长链接地址 |
| `expired_time` | timestamp | 到期时间 · 可空 |
| `jump_type` | varchar(5) | 跳转类型（301 永久重定向，302临时重定向） |
| `use_type` | varchar(32) | 使用类型 · 可空 |
| `type` | varchar(10) | 类型 系统加密存储 E，系统明文存储 P，自定义短链接码 C |
| `create_time` | timestamp(3) | 创建时间 |
| `update_time` | timestamp(3) | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `uk_short_link_code`:code (UNIQUE)
- `idx_short_link_expired_time`:expired_time

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
