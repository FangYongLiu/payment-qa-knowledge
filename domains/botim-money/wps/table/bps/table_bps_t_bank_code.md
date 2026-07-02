---
id: tbl_bps_t_bank_code
object_type: Table
name: 工资卡号信息表 (t_bank_code)
aliases: [t_bank_code, bps.t_bank_code]
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

# 工资卡号信息表 (t_bank_code)

## 用途
物理表 `bps.t_bank_code`,主键 `id`。工资卡号信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | char(3) | 主键 |
| `entity_name` | varchar(256) | 银行全称 |
| `entity_type` | char(10) | 银行类型 |
| `entity_short_name` | varchar(32) | 银行简称 |
| `swift_code8` | char(8) | 8位标识 |
| `swift_code11` | char(11) | 11位标识 |
| `local_clearing_code` | char(10) | 路由编号 |
| `cbid_code` | char(10) | 中央银行编号 |
| `createAt` | timestamp | 创建时间 |
| `updateAt` | timestamp | 更新时间 |

## 主键 / 索引
- 主键:`id`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
