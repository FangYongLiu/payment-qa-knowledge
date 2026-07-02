---
id: tbl_pfs_tb_prov_info
object_type: Table
name: 稳定，100行 (tb_prov_info)
aliases: [tb_prov_info, pfs.tb_prov_info]
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

# 稳定，100行 (tb_prov_info)

## 用途
物理表 `pfs.tb_prov_info`,主键 `PROV_ID`。稳定，100行。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `PROV_ID` | decimal(15) | 省份Id |
| `PROV_NAME` | varchar(128) | 省份全称 |
| `PROV_SHORTNAME` | varchar(128) | 省份简称 |
| `PROV_ALIASES` | varchar(256) | 省份别名 · 可空 |
| `EXTENSIONS` | varchar(512) | 扩展信息 · 可空 |
| `ENABLE_FLAG` | char | 启用标识 |
| `MEMO` | varchar(256) | 备注 · 可空 |
| `VERSION` | decimal(15) | 版本 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFY` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`PROV_ID`
- `UK_PROVINFO_PROVNAME`:PROV_NAME (UNIQUE)
- `UK_PROVINFO_PROVSHORTNAME`:PROV_SHORTNAME

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
