---
id: tbl_mchtsettle_t_clearing_file
object_type: Table
name: 清算文件表 (t_clearing_file)
aliases: [t_clearing_file, mchtsettle.t_clearing_file]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: mchtsettle schema DDL
tags: [online-business, 商户结算, mchtsettle]
sensitivity: normal
related_services: [svc_merchant_settlement]
---

# 清算文件表 (t_clearing_file)

## 用途
物理表 `mchtsettle.t_clearing_file`,主键 `id`。clearing file。属商户结算服务 [[svc_merchant_settlement]]。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:[[svc_merchant_settlement]](= `related_services`)。
- **谁读写它**:结算链路的服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | id |
| `batch_id` | bigint | batch id |
| `file_md5` | varchar(200) | file_md5 · 可空 |
| `file_name` | varchar(200) | file_name |
| `file_oss_path` | varchar(200) | file oss path |
| `status` | varchar(16) | status |
| `created_time` | timestamp(3) | created_time |
| `last_updated_time` | timestamp(3) | last_updated_time |
| `data_version` | bigint | data_version |
| `origin_file_name` | varchar(200) | origin_file_name · 可空 |

## 主键 / 索引
- 主键:`id`
- `uk_file_oss_path`:file_oss_path (UNIQUE)
- `uk_tcf_ofn`:origin_file_name (UNIQUE)
- `i_batch_id_status`:batch_id, status

## 校验点(QA 关注)
- **时间字段**:`created_time`=入库、`last_updated_time`=最后更新;按时间过滤走对应索引。
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- **乐观锁**:更新须带 `data_version`,并发场景校验版本递增。
- **批次维度**:`batch_id` 关联清算批次 t_clearing_batch。
- 更细的状态枚举、跨表关联与业务规则**待补**(需结合代码或业务文档)。
