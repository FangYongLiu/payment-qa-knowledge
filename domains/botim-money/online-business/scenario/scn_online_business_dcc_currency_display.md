---
id: scn_online_business_dcc_currency_display
object_type: Scenario
name: DCC 收银台币种图标与结果页免责声明
aliases: [DCC currency icons, DCC disclaimer currency]
domain: online-business
status: draft
owner: fangyong.liu
reviewer: fangyong.liu
last_reviewed_at: '待补'
source_type: jira
source_ref: PAYM-3078
tags: [dcc, checkout, currency, disclaimer, acquiring]
related_services: []          # svc_hive_checkout(gp048)服务对象未入仓,不加死指针;见正文「待补」
related_tables: [tbl_acquireii_t_dcc_info]
related_logs: []
---

# DCC 收银台币种图标与结果页免责声明

外卡持卡人在收银台选择 DCC(动态货币转换)币种时,币种选择卡应显示对应国旗;支付结果页的
币种免责声明应显示用户**实际选中**的币种,而非硬编码 `[USD]` 占位符。

## 触发 / 入口
- 收银台 `hive-checkout`(gp048)DCC 币种选择页 + 支付结果页免责声明区。
- 对应 cgs-apitest 用例:待补(此为前端展示校验;Zephyr UAT 用例 PAYM-T17237~T17241)。

## 关联关系
- **涉及服务**:收银台前端 `hive-checkout`(gp048,`svc_hive_checkout` 服务对象**待补**——尚未入仓,补入后填 `related_services` 并在此加 `[[svc_hive_checkout]]`);ToB 收单网关见 [[svc_sgs]]。
- **校验的表**:[[tbl_acquireii_t_dcc_info]](选中币种 / 汇率落库;免责声明币种须与此一致)。
- **测它的接口 / 覆盖它的自动化**:待补。

## 前置条件
- 交易为外卡、命中 DCC,且用户**接受** DCC(`t_dcc_info` 有完整数据、`dcc_uptake`=接受)。
- 所选币种在「币种→国家/地区」映射表中(PAYM-3078 新增约 150 个币种映射,如 HKD/THB/SGD/BRL/XOF)。

## 操作步骤
1. 进入收银台 DCC 币种选择页,查看各币种卡的国旗图标。
2. 抽查新映射币种(如 THB/SGD/BRL/XOF)的国旗是否正确、非空白。
3. 选择一个非本币(如 HKD)完成支付,查看结果页 DCC 免责声明。
4. 回归:非 DCC / 拒绝 DCC 的流程不受影响。

## DB 校验点
- [[tbl_acquireii_t_dcc_info]]:记录本单选中的 DCC 币种;结果页免责声明显示的币种须与该记录一致。
- 免责声明**不得**出现硬编码 `[USD]`,也不得出现任何未替换的 `[...]` 占位符。

## 预期结果
- 每个映射币种卡显示正确国旗(如 HKD 显示香港旗);修复 `MRCHNT-1548`(HKD 旗标缺失)后不再复现。
- 结果页免责声明显示用户实际选中币种(HKD),无 `[USD]` 占位符;修复 `MRCHNT-1552`(结果页免责声明硬编码 `[USD]`)。
- 免责声明币种与上方币种转换区块一致。
- 非 DCC / declined-DCC 交易不受影响(回归护栏)。
> 由 PAYM-3078(关联 bug MRCHNT-1548 / MRCHNT-1552)蒸馏,5 条前端用例 PAYM-T17237~T17241 按业务流并为本场景。服务对象 `svc_hive_checkout`、具体校验接口、自动化覆盖均标「待补」,待人工核对后补全。
