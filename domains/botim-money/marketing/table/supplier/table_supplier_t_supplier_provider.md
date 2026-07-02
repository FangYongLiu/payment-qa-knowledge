---
id: tbl_supplier_t_supplier_provider
object_type: Table
name: 供应商信息表 (t_supplier_provider)
aliases: [t_supplier_provider, supplier.t_supplier_provider]
domain: marketing
status: active
owner: wujiang.ding
reviewer: wujiang.ding
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: supplier schema DDL
tags: [marketing, supplier]
sensitivity: normal
related_services: []
---

# 供应商信息表 (t_supplier_provider)

## 用途
物理表 `supplier.t_supplier_provider`,主键 `ID`。供应商信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint(32) | 待补 · 可空 |
| `PROVIDER_CODE` | varchar(32) | 供应商编号 |
| `PROVIDER_NAME` | varchar(64) | 供应商名称 · 可空 |
| `COUNTRY_CODE` | varchar(32) | 国家编号 |
| `validation_regex` | varchar(128) | 正则表达 · 可空 |
| `Region_Codes` | varchar(255) | 地区编号 |
| `Logo_Url` | varchar(255) | logo地址 · 可空 |
| `STATUS` | varchar(16) | 是否可用：VALID（可用），INVALID（不可用） |
| `COMMISSION_TYPE` | char | Commission Type · 可空 |
| `COMMISSION_CONTENT` | varchar(8) | Commission Content · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 · 可空 |
| `MEMO` | varchar(255) | 备注 · 可空 |
| `supplier_no` | varchar(32) | 供应商编号 |
| `service_provider` | varchar(32) | 服务提供商 · 可空 |
| `catalog_version` | varchar(16) | catalog版本号 · 可空 |

## 主键 / 索引
- 主键:`ID`
- `uk_providerCode_supplierNo_country`:PROVIDER_CODE, supplier_no, COUNTRY_CODE (UNIQUE)

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
