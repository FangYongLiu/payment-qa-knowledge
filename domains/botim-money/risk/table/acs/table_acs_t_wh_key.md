---
id: tbl_acs_t_wh_key
object_type: Table
domain: risk
status: active
owner: xinwei.cao,dewen.li
reviewer: xinwei.cao,dewen.li
last_reviewed_at: '2026-06-25'
source_type: DB DDL
source_ref: DataGrip DDL export (acs schema) 2026-06-25
tags:
- acs
- acs
- t_wh_key
subdomain: acs
module: null
sensitivity: normal
name: 钱包密钥管理(t_wh_key)
aliases:
- t_wh_key
related_services:
- svc_acs
related_scenarios: []
---
# 钱包密钥管理(t_wh_key)

## 用途
钱包密钥管理。属 acs 库,由 [[svc_acs]] 读写。

## 关联关系
- **所属服务**:[[svc_acs]](= `related_services`)
- **谁读写它**:读写本表的服务 / 接口,在各自文档的 `related_tables` 中列出(本表侧不重复)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 约束 | 说明 |
| --- | --- | --- | --- |
| `ID` | decimal(8) | PK / NOT NULL | pk，由SEQ_MERCHANT_KEY生成 |
| `CERTIFICATE` | varchar(4000) |  | 证书内容 |
| `CERT_TYPE` | decimal(8) |  | 证书类型 |
| `CERT_FORMAT` | varchar(40) |  | 证书格式 |
| `ALGORITHM` | varchar(20) | NOT NULL | 加密算法 |
| `VERSION` | varchar(20) | NOT NULL | 版本号 |
| `EXT` | varchar(400) |  | 扩展字段 |
| `REMARK` | varchar(400) |  | 备注 |
| `CREATE_TIME` | timestamp |  | 创建时间 |
| `LAST_MODIFIED_TIME` | timestamp |  | 最后更新时间 |
| `MERCHANT_ID` | varchar(20) |  | 商户ID |
| `PUBLIC_KEY` | varchar(2000) |  | 微汇公钥 |

## 主键 / 索引
- 主键:(`ID`)
- 索引:无(或见 DDL)

## 校验点(QA 关注)
- 落库检查、状态流转、与上下游表/接口一致性。
- 不确定的标「待补」,留人工补充。
