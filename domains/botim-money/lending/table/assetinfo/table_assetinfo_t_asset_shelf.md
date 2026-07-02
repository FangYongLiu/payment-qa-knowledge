---
id: tbl_assetinfo_t_asset_shelf
object_type: Table
name: 货架配置 (t_asset_shelf)
aliases: [t_asset_shelf, assetinfo.t_asset_shelf]
domain: lending
status: active
owner: Xiaopei.Yan
reviewer: Xiaopei.Yan
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: assetinfo schema DDL
tags: [lending, assetinfo]
sensitivity: normal
related_services: []
---

# 货架配置 (t_asset_shelf)

## 用途
物理表 `assetinfo.t_asset_shelf`,主键 `id`。货架配置。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `rank` | bigint | rank |
| `asset_info_code` | varchar(32) | 资产代码 |
| `created_time` | timestamp(3) | 创建时间 |
| `last_updated_time` | timestamp(3) | 最后更新时间 |
| `data_version` | bigint | 数据版本 |

## 主键 / 索引
- 主键:`id`
- `uk_as_code`:asset_info_code (UNIQUE)
- `uk_as_rank`:`rank` (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- **乐观锁**:更新须带 `data_version`,并发校验版本递增。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
