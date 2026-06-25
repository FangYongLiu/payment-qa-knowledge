---
id: ts_enbd_channel_balance_not_enough
object_type: Troubleshooting
name: ENBD 出款报 channel account balance is not enough
aliases: [ENBD余额不足, ENBD出款排查]
domain: channel
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:tester/1064206364
tags: [enbd, fundout, 出款, 余额校验, 排查]
related_services: [svc_qpay_enbd]
related_tables: []
related_logs: []
related_failures: []
---

# ENBD 出款报 channel account balance is not enough

## 症状
router 日志出现 `ENBD 渠道 channel account balance is not enough` 报错,出款被余额校验拦截。

## 关联关系
- **涉及服务 / 表**:[[svc_qpay_enbd]] / cmf / router(后两者对象待补);`router.t_channel_ext`、`reconciliation.t_balance_history`(对象待补)
- **相关日志**:`开始 余额监控 定时任务`(余额监控 job)
- **出款流程**:[[flow_enbd_fundout]]

## 可能根因
- 余额查询不准 / 缓存陈旧;对方系统瞬时波动导致校验失败;余额监控 job 未正常运行或规则配置缺失。

## 排查步骤
1. **确认余额查询是否正常**,两种方式核对:
   - 查 counter 中该渠道账户的最新余额数据;
   - 查 Redis 缓存 key `_cmf:accountBalance:XXXXX`(XXXXX 为渠道账号)。
2. **确认渠道是否配置 payoutAccount**(router 仅在配置了 payoutAccount 的渠道做余额校验):
   ```sql
   select * from router.t_channel_ext
   where channel_code in ('ENBD201','ENBD204','ENBD205')
     and attr_key = 'payoutAccount';
   ```
3. **确认余额监控 job 是否正常运行**:日志关键字「开始 余额监控 定时任务」,落库 `reconciliation.t_balance_history`(余额无变化不新增)。
4. **确认 balance monitor 规则配置**:counter – account – balance monitor;注意一期规则和交易阈值共用数据,**一个账户只能配置一条规则**。
5. **确认渠道与银行交互状态**:见 [[flow_enbd_fundout]] 状态流转(`httpResponseStatus=202` / `ACCEPTED` / `IN_PROGRESS` / `PROCESSED_BY_BANK` / `COMPLETED`)。

## 处理 / 规避
- 若余额数据正常(充足且与实际相符),可再次发起出款——多为当时对方系统波动导致的瞬时校验失败。
- 测试环境可用 IBAN:EBILAED `AE780260001015795438201`;MEBLAED `AE800340003707336602101`;FGBMAEAA `AE780271091001071667018`。
