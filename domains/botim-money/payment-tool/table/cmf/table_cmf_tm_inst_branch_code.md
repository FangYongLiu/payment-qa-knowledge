---
id: tbl_cmf_tm_inst_branch_code
object_type: Table
name: 机构分支行编码表 (tm_inst_branch_code)
aliases: [tm_inst_branch_code, cmf.tm_inst_branch_code]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cmf schema DDL
tags: [payment-tool, cmf]
sensitivity: normal
related_services: []
---

# 机构分支行编码表 (tm_inst_branch_code)

## 用途
物理表 `cmf.tm_inst_branch_code`,主键 `BRANCH_CODE`。机构分支行编码表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `INST_CODE` | varchar(16) | 机构代码 |
| `BRANCH_NAME` | varchar(128) | 分支名称 |
| `BRANCH_CODE` | varchar(32) | 分支代码 |
| `PARENT_CODE` | varchar(32) | 上级分支代码 |
| `GMT_CREATE` | timestamp | 创建时间 |

## 主键 / 索引
- 主键:`BRANCH_CODE`
- 无(仅主键)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
