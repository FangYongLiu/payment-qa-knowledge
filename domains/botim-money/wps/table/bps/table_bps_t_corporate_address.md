---
id: tbl_bps_t_corporate_address
object_type: Table
name: 公司地址表 (t_corporate_address)
aliases: [t_corporate_address, bps.t_corporate_address]
domain: wps
status: active
owner: xinwei.cao
reviewer: xinwei.cao
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: bps schema DDL
tags: [wps, bps]
sensitivity: normal
related_services: []
---

# 公司地址表 (t_corporate_address)

## 用途
物理表 `bps.t_corporate_address`,主键 `id`。公司地址表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(32) | 主键 |
| `corporate_country` | varchar(64) | 公司国家 |
| `corporate_city` | varchar(128) | 公司城市 |
| `corporate_detail_address` | varchar(256) | 公司详细地址 |
| `data_version` | bigint | 版本号 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
