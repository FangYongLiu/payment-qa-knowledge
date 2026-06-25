---
id: scn_channel_prerelease_collaboration
object_type: Scenario
name: PayBy 渠道发布前 Dev-Test-Product 协作流程(6 步)
aliases: [渠道发布协作, channel pre-release process, Go-Live Checklist]
domain: channel
status: active
owner: unassigned
reviewer: unassigned
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/1467416579; wiki:90d0e5a2-d7f3-4451-9ca3-4c76d0f489ab
tags: [channel, release, collaboration, go-live, QA-process]
related_services: []
related_tables: []
related_logs: []
---

# PayBy 渠道发布前 Dev-Test-Product 协作流程(6 步)

## 触发 / 入口
渠道类需求发布前,从功能范围对齐到上线就绪检查的 6 步协作流程,明确 Dev/QA/PM/PMO 在每一步的职责与产出物(Evidence,均沉淀到 JIRA),确保发布质量可追溯。

## 关联关系
- **角色**:Dev、QA、Product Manager、PMO
- **适用**:全部渠道接入需求(本域各渠道通用)

## 操作步骤(6 步)
### Step 1:Functional Scope Alignment(功能范围对齐)
- Owners:Dev & QA。
- Dev:列出代码改动、新增 API、下线 endpoint,在 JIRA 描述补充细节与影响范围。
- QA:定义测试范围和回归集,附 test cycle 链接。

### Step 2:Test Environment & Smoke Strategy(环境与冒烟策略)
- Owner:QA。核心原则:**未在渠道真实 sandbox 中测试过的,不算测过。**
- Mock 仅限异常路径或第三方暂不可用;Smoke 与正式测试必须在 **channel supplier 的 test 环境**执行。

### Step 3:Post-SIM Code-Hardening(SIM 后代码加固)
- Owner:Dev。**SIM 退出后、UAT 之前至少预留半天窗口**。
- Code review & merge(Jira 记录评审时间/人/结论);Config review vs prod(独立配置项记录各环境配置);CR validation(每条 Jira 评论 "CR-verified",高亮环境差异值)。

### Step 4:UAT Result & Log Verification(UAT 结果与日志验证)
- Owners:Dev(QA 协助)。
- QA:建立 Test-case ↔ Order-ID 映射,每个 test cycle 附结果,核心用例结果写入 Jira 评论。
- Dev:对提交订单数据做业务逻辑校验,Jira 评论追加 "verification-passed"。

### Step 5:Product Sign-off(产品验收签收)
- Owner:PM。QA 跟进推动 UAT 按期进行;PM 完成功能验收并在 JIRA 评论 "verification-passed"。

### Step 6:Go-Live Readiness Checklist(上线就绪检查)
- Owner:PMO。上线前各角色在 JIRA 逐项验证并留痕。

| # | 检查项 | Verified by | Evidence |
|---|---|---|---|
| 6.1 | UAT 在 channel-supplier UAT 环境执行完毕 | Dev + QA | Test cycle link |
| 6.2 | Key-Vault 值已注入 | Key Manager | Jira 评论附确认截图 |
| 6.3 | 最终 config + CR 值已复核 | Dev | 评论 "config-verified" / "CR-verified" |
| 6.4 | 影响说明 + 生产验证脚本 | Dev + QA + Product | 生产验证计划附在 Jira ticket |
| 6.5 | 监控与告警已启用(失败、SLA 违约) | Dev | 附 Grafana alert export JSON |
| 6.6 | 回滚方案已编写并演练 | Dev + QA + Product | 回滚方案文档附在 Jira ticket |

## DB / 校验点
- 不涉及 DB;以 JIRA Evidence(评论、附件、test cycle 链接、截图、JSON 导出)为追溯依据。

## 预期结果
- 关键约束:Smoke/正式测试一律在渠道供应商测试环境;Mock 仅限异常路径或第三方不可用;SIM→UAT 间预留至少半天加固窗口;每步 Evidence 落 JIRA。
