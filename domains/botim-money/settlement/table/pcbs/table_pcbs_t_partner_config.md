---
id: tbl_pcbs_t_partner_config
object_type: Table
name: Partner Config (t_partner_config)
aliases: [t_partner_config, pcbs.t_partner_config]
domain: settlement
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pcbs schema DDL
tags: [settlement, pcbs]
sensitivity: normal
related_services: []
---

# Partner Config (t_partner_config)

## 用途
物理表 `pcbs.t_partner_config`,主键 `partner_id`。Partner Config。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `partner_id` | varchar(20) | Partner ID |
| `partner_code` | varchar(20) | Partner Code |
| `partner_name` | varchar(100) | Partner Name |
| `processor_code` | varchar(32) | Processor Code: NYMCARD=NymCard |
| `pre_fund_loading_mid` | varchar(20) | Pre Fund Loading Merchant ID |
| `customer_loading_mid` | varchar(20) | Customer Loading Merchant ID |
| `extension` | varchar(255) | Extension · 可空 |
| `enable_flag` | char | Enable Flag: Y=Yes, N=No |
| `create_time` | timestamp | Create time |
| `update_time` | timestamp | Update time |

## 主键 / 索引
- 主键:`partner_id`
- `uk_partner_code`:partner_code (UNIQUE)

## 校验点(QA 关注)
- **时间字段**:创建/更新时间;按时间过滤走对应索引。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
