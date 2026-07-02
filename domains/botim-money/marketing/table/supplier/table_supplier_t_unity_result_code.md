---
id: tbl_supplier_t_unity_result_code
object_type: Table
name: 统一结果码 (t_unity_result_code)
aliases: [t_unity_result_code, supplier.t_unity_result_code]
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

# 统一结果码 (t_unity_result_code)

## 用途
物理表 `supplier.t_unity_result_code`,主键 `ID`。统一结果码。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint(32) | 待补 · 可空 |
| `SUPPLIER_NO` | varchar(32) | 供应商编号 |
| `UNITY_RESULT_CODE` | varchar(32) | 统一结果编码 |
| `DESCRIPTION_TEMPLATE` | varchar(32) | 描述模板 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 · 可空 |
| `MEMO` | varchar(255) | 备注 · 可空 |
| `RESULT_CODE` | varchar(32) | 结果码 · 可空 |
| `SUB_RESULT_CODE` | varchar(32) | 结果子码 · 可空 |
| `RESULT_STATUS` | varchar(4) | 订单状态 · 可空 |
| `ENABLE_FLAG` | char | 是否启用 · 可空 |
| `EXTENSION` | varchar(128) | 扩展参数 · 可空 |

## 主键 / 索引
- 主键:`ID`
- `uk_result_code`:SUPPLIER_NO, RESULT_CODE, SUB_RESULT_CODE (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
