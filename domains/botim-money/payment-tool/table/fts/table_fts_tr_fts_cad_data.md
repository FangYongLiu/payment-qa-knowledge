---
id: tbl_fts_tr_fts_cad_data
object_type: Table
name: wps写入CAD数据 (tr_fts_cad_data)
aliases: [tr_fts_cad_data, fts.tr_fts_cad_data]
domain: payment-tool
status: active
owner: kingo.liang
reviewer: kingo.liang
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: fts schema DDL
tags: [payment-tool, fts]
sensitivity: normal
related_services: []
---

# wps写入CAD数据 (tr_fts_cad_data)

## 用途
物理表 `fts.tr_fts_cad_data`,主键 `id`。wps写入CAD数据。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `id` | bigint | 唯一标识符 · 可空 |
| `source` | varchar(32) | 系统来源,比如wps |
| `request_no` | varchar(32) | wps请求号，相当于幂等id |
| `data_no` | varchar(32) | 自己生成的唯一数据编号 |
| `member_id` | varchar(20) | 会员id · 可空 |
| `entity_id` | char(3) | default 413在ubuae唯一标号 |
| `account_type` | char | 1-Current Account,2-Savings Account,3-Card Account,4-Internal Accounts,5-All Other Types of Accounts,6-Registered Customer |
| `account_classification` | char(3) | IRE-Individual (Resident),INR-Individual (Non-Resident),JUR-Juridical,INT-Internal |
| `account` | varchar(16) | iban后16位 · 可空 |
| `iban` | varchar(30) | 待补 · 可空 |
| `currency` | char(3) | AED · 可空 |
| `title` | varchar(100) | 用户姓名 · 可空 |
| `account_eac` | varchar(5) | default 0802/，金融机构其他 · 可空 |
| `id_type` | char(2) | default XX,认证的证件类型 · 可空 |
| `id_number` | varchar(50) | default XXXXXXXXX,证件号 · 可空 |
| `balance_or_limit` | varchar(18) | default 0.00,账户限额 · 可空 |
| `account_status` | char | A-ACtive,D-Dormant,C-Closed,B-Blocked,X-Deceased · 可空 |
| `status` | varchar(8) | INITIAL,SUCCESS,FAILED · 可空 |
| `state` | varchar(8) | INIT,PROCESS,SUCCESS,FAILED,NOTIFIED,这条数据上传状态流转 · 可空 |
| `batch_no` | varchar(32) | 文件批次号 · 可空 |
| `line_no` | char(6) | file line no文件行号 · 可空 |
| `extension` | varchar(1024) | 待补 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_update` | timestamp | 修改时间 |

## 主键 / 索引
- 主键:`id`
- `udx_fcd_source_rq`:source, request_no (UNIQUE)
- `idx_fcd_bn_ln`:batch_no, line_no
- `idx_fcd_create`:gmt_create
- `idx_fcd_data_no`:data_no

## 校验点(QA 关注)
- **状态字段**:`status` 合法枚举与流转规则需结合代码/业务文档核对(**待补**)。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
