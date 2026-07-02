---
id: tbl_pcm_t_pcm_pay
object_type: Table
name: 付款码支付信息表 (t_pcm_pay)
aliases: [t_pcm_pay, pcm.t_pcm_pay]
domain: payment-core
status: active
owner: xiaoyan.zhou
reviewer: xiaoyan.zhou
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: pcm schema DDL
tags: [payment-core, pcm]
sensitivity: normal
related_services: []
---

# 付款码支付信息表 (t_pcm_pay)

## 用途
物理表 `pcm.t_pcm_pay`,主键 `ID`。付款码支付信息表。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `ID` | bigint(17) | 待补 |
| `GID` | varchar(32) | 订单号 |
| `VERIFY_PWD` | tinyint(2) | 是否需要验密 |
| `DECODE_PCC_FINAL` | varchar(255) | 编码之后的PCCT |
| `RISK_RESULT` | varchar(100) | 风控结果 |
| `ACCOUNT_TOKEN` | varchar(32) | 帐号TOEKN |
| `MEMBER_ID` | varchar(50) | 会员ID |
| `DEVICE_ID` | varchar(255) | 设备ID |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 修改时间 |
| `HOST_APP` | varchar(50) | 宿主应用 |
| `auth_status` | tinyint | 授权状态：1：成功 0：失败 |
| `error_log` | varchar(500) | 错误日志 · 可空 |
| `i18_code` | varchar(120) | 文案key · 可空 |

## 主键 / 索引
- 主键:`ID`
- `uk_gid`:GID (UNIQUE)
- `idx_decode_pcc_final`:DECODE_PCC_FINAL
- `idx_t_pcm_pay_memberid`:MEMBER_ID

## 校验点(QA 关注)
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
