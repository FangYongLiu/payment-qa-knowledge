---
id: tbl_cmf_tb_card_token
object_type: Table
name: 卡token表 (tb_card_token)
aliases: [tb_card_token, cmf.tb_card_token]
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

# 卡token表 (tb_card_token)

## 用途
物理表 `cmf.tb_card_token`,主键 `card_token_id`。卡token表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `card_token_id` | bigint | 卡tokenId |
| `inst_order_id` | bigint(32) | 机构订单id · 可空 |
| `token_type` | varchar(10) | token类型 · 可空 |
| `member_id` | varchar(32) | 会员id |
| `card_id` | bigint(15) | 卡id · 可空 |
| `beneficiary_id` | bigint(15) | 受益人id · 可空 |
| `session_id` | varchar(32) | sessionID · 可空 |
| `inst_code` | varchar(16) | 目标机构 · 可空 |
| `dbcr` | char(2) | 借记贷记 DC借记 CC贷记 · 可空 |
| `company_or_personal` | char | 对公对私 B对公 C对私 · 可空 |
| `issue_bank` | varchar(4) | 发卡行 · 可空 |
| `is_3ds` | char | is3ds · 可空 |
| `first_bind` | char | 首次绑卡, Y-是,N-否 · 可空 |
| `need_csc` | char | Y-need,N-not · 可空 |
| `ip_address` | varchar(40) | customer ip address,ipv4 or ipv6 · 可空 |
| `iban` | varchar(32) | iban · 可空 |
| `extension` | varchar(1024) | 扩展参数 · 可空 |
| `gmt_create` | timestamp | 创建时间 |
| `gmt_modified` | timestamp | 修改时间 · 可空 |
| `card_no` | varchar(32) | 卡号 · 可空 |
| `card_account_no` | varchar(32) | 卡账号 · 可空 |
| `country_code` | varchar(3) | 国家编码 · 可空 |
| `card_holder` | varchar(256) | 持卡人 · 可空 |
| `inst_token_id` | varchar(32) | 机构tokenId · 可空 |
| `card_expired` | varchar(32) | 卡片有效期 · 可空 |
| `expired_month` | varchar(2) | 有效期-月份 · 可空 |
| `expired_year` | varchar(2) | 有效期-年份 · 可空 |
| `card_type` | varchar(2) | 卡类型 · 可空 |
| `card_brand` | varchar(16) | 卡品牌 · 可空 |
| `result_url` | varchar(255) | 结果url · 可空 |

## 主键 / 索引
- 主键:`card_token_id`
- `uk_card_token_order_id`:inst_order_id (UNIQUE)

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
