---
id: tbl_cspayment_tb_clearing_session_06
object_type: Table
name: 清算场次 (tb_clearing_session_06)
aliases: [tb_clearing_session_06, cspayment.tb_clearing_session_06]
domain: online-business
status: active
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '2026-07-02'
source_type: DB DDL
source_ref: cspayment schema DDL
tags: [online-business, cspayment]
sensitivity: normal
related_services: []
---

# 清算场次 (tb_clearing_session_06)

## 用途
物理表 `cspayment.tb_clearing_session_06`,主键 `CLEARING_SESSION_ID`。清算场次。业务语义细节**待补**(表结构来自 DDL)。

## 关联关系
- **所属服务**:待补。
- **谁读写它**:相关服务 / 接口(由对方文档 `related_tables` 声明)。
- **哪些场景校验它**:待补。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| `CLEARING_SESSION_ID` | varchar(32) | 清算场次标识:SEQ_CLEARING_SESSION_ID |
| `SESSION_LEVEL` | varchar(8) | 层次，大类前缀：O-外场；I-内场 |
| `SESSION_TYPE` | char | 场次类型：R-实时；T-时间触发；O：外部触发； |
| `EXECUTE_STATUS` | char | 执行状态：W-待执行；P-执行中；S-成功；F-失败；E-异常；Z-已暂停；C-已取消 |
| `GMT_BOOKING_SHOW` | timestamp | 预订出场时间 · 可空 |
| `GMT_SHOW` | timestamp | 出场时间 · 可空 |
| `BATCH_NO` | varchar(32) | 批次号 · 可空 |
| `RETRY_TIMES` | decimal(3) | 重试次数 · 可空 |
| `NEED_RETRY` | char | 是否重试：Y-是；N-否 · 可空 |
| `GATHER_TYPE` | char | 汇总类型：N-不汇总；G-汇总；O-轧差；B-批量 |
| `GMT_CREATE` | timestamp | 创建时间 |
| `GMT_MODIFIED` | timestamp | 最后修改时间 |
| `MEMO` | varchar(128) | 备注 · 可空 |

## 主键 / 索引
- 主键:`CLEARING_SESSION_ID`
- `IDX_CS_BATCH_NO_06`:BATCH_NO
- `IDX_CS_GMT_BOOKING_SHOW_06`:GMT_BOOKING_SHOW

## 校验点(QA 关注)
- **金额精度**:decimal 比较用容差(< 0.01);amount 与 currency 需一致。
- 业务语义、状态枚举、跨表关联**待补**(需结合代码或业务文档)。
