---
id: tbl_pfs_tb_area_info
object_type: Table
name: 稳定，10000行 (tb_area_info)
aliases: [tb_area_info, pfs.tb_area_info]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pfs schema DDL
tags: [payment-core, pfs]
sensitivity: normal
related_services: []
---

# 稳定，10000行 (tb_area_info)

## 用途
物理表 `pfs.tb_area_info`,主键 `AREA_CODE`。稳定，10000行。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `AREA_CODE` | char(4) | 地区代码 |
| `AREA_NAME` | varchar(128) | 地区全称 |
| `AREA_SHORTNAME` | varchar(128) | 地区简称 |
| `AREA_ALIASES` | varchar(256) | 地区别名 · 可空 |
| `PROV_ID` | decimal(15) | 所属省份Id · 可空 |
| `CITY_ID` | decimal(15) | 所属城市Id · 可空 |
| `EXTENSIONS` | varchar(512) | 扩展信息 · 可空 |
| `ENABLE_FLAG` | char | 启用标识：Y=启用，N=停用 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `VERSION` | decimal(15) | 版本 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`AREA_CODE`
- `I_AREAINFO_VERSION`:VERSION

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
