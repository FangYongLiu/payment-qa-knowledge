---
id: tbl_cmf_tb_card_black_list
object_type: Table
name: 卡号黑名单表 (tb_card_black_list)
aliases: [tb_card_black_list, cmf.tb_card_black_list]
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

# 卡号黑名单表 (tb_card_black_list)

## 用途
物理表 `cmf.tb_card_black_list`,主键 `LIST_ID`。卡号黑名单表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `LIST_ID` | decimal(12) | id |
| `INST_ORDER_NO` | varchar(32) | 机构订单号 · 可空 |
| `FUND_CHANNEL_CODE` | varchar(32) | 渠道编号 |
| `CARD_NO` | varchar(32) | 卡号 |
| `OPERATOR` | varchar(32) | 操作员 · 可空 |
| `MEMO` | varchar(64) | 备注 · 可空 |
| `EXTENSION` | varchar(256) | 扩展 · 可空 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 · 可空 |
| `CARD_TYPE` | char | 卡类型：I:cardID类型;N:cardNo类型 默认N · 可空 |
| `GMT_EXPIRE` | timestamp | 过期时间 · 可空 |

## 主键 / 索引
- 主键:`LIST_ID`
- `UK_CARD_BLIST_CDNO_CHCODE`:CARD_NO, FUND_CHANNEL_CODE (UNIQUE)
- `I_CARD_BLACK_LIST_CHANNELCODE`:FUND_CHANNEL_CODE

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
