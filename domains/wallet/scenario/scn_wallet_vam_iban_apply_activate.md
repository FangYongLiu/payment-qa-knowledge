---
id: scn_wallet_vam_iban_apply_activate
object_type: Scenario
name: VAM IBAN 虚拟账户申请激活与交易通知 (VAM IBAN Apply / Activate / Notify)
aliases: [VAM IBAN, 虚拟银行账户激活, Virtual Bank Account Activation, Bank Account Transfer 充值]
domain: wallet
status: active
owner: qianlong.wang
reviewer: qianlong.wang
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: legacy/wiki/vam-iban (vam-iban-overview / scn_vam_iban_apply_activate / scn_vam_iban_apply_and_transaction)
tags: [wallet, vam, iban, vis, fab, 虚拟账户, 充值]
related_services: [svc_vis, svc_deposit]
related_tables: [tbl_vis_t_virtual_account, tbl_vis_t_notify_transaction_flow]
related_logs: []
---

# VAM IBAN 虚拟账户申请激活与交易通知

> 业务测试场景。来源:归档 wiki/vam-iban。VAM(Virtual Account Management)IBAN 是 PayBy 与 FAB(First Abu Dhabi Bank)合作的虚拟银行账户,用户激活后可通过 **Bank Account Transfer**(银行转账)向自己的 PayBy 钱包充值,亦支持 WPS 收薪、国际转账收款。账户能力由 [[svc_vis]] 提供。

## 触发 / 入口
- PayBy App → **Recharge(充值)** → 选择 **Bank Account Transfer** → 点击激活
  - 充值页 Recharge Via 共三种入口:Debit Card / uPay Kiosks / **Bank Account Transfer**(VAM IBAN 场景的重点入口)。
- 激活页(Activate Virtual Bank Account)提供两个激活入口:顶部横幅 `Active Now >` 与底部全宽 `Free Active` 按钮。
- VIP 用户:点击 **Free Active** 后需补充姓名信息(姓名**无校验**)。
- 交易通知模拟入口(Fitnesse):`http://fitnesse.test2pay.com/FrontPage.VisSuitePage.VisNotifyFacade.TestCaseN101`。

## 关联关系
- **涉及服务**:[[svc_vis]](虚拟 IBAN 账户服务)、[[svc_deposit]](充值入账)(= `related_services`)
- **校验的表**:[[tbl_vis_t_virtual_account]](虚拟账户主记录)、[[tbl_vis_t_notify_transaction_flow]](交易通知流水)(= `related_tables`)
- **批次重试 Job**:`vis_ibanAccountRetryJob`(对应自动化资产「待补」,原 wiki 引用的 `auto_vis_iban_account_retry_job` 当前库中不存在,故不连边)
- **运营控台**:Counter System → VIS Management(File Flow / Virtual IBAN Account / Transaction Flow / ...),详见下文。

## 前置条件
- 用户已登录 PayBy App,具备充值入口。
- 区分用户类型:普通 fab 用户、VIP 用户、lean 场景用户。
- IBAN 库存可用(无库存场景需人工补录,见下)。
- 不调用 fab 的本地 mock 配置:
  ```yaml
  vis:
    notification:
      mock: Y
  ```

## 操作步骤
1. 进入充值页,选择 **Bank Account Transfer**,点击激活(VIP 用户为 Free Active,需补充姓名)。
2. 前端展示三种状态之一:
   - **激活成功**:展示 IBAN 信息。
   - **激活处理中**:进入批次处理,等待 Job 重试。
   - **无 IBAN 信息**:IBAN 库存不足时,落库不带 IBAN。
3. 批次处理:除 **lean 场景**(直接处理,绕过批次)外,其他 fab 用户申请均走批次,由 Job `vis_ibanAccountRetryJob` 触发——打批发 fab,将 IBAN 数据状态更新为 `Valid`。
4. 库存不足:落库无 IBAN,需按「人工补录 IBAN」规范补充数据后等待 Job 重试(原文提及可联系 wangqian 人工添加,人员信息「待补 / 以实际为准」)。
5. 交易通知:通过 Fitnesse 用例 `TestCaseN101` 模拟发送交易通知,验证流水落库。

## 人工补录 IBAN 数据(导入模板规范)
当 IBAN 库存为空、需人工补录时,按以下 Excel 模板字段提供数据(首行为列头):

| 列 | 字段 | 示例 | 填写规范 |
|----|------|------|----------|
| A | Virtual Account Entity Identifier | `40006` | 实体标识,按模板原样维护 |
| B | Virtual Account ID | `00000112` | **从末位开始修改**,使其对应 `vis` 账户表里的 id;例如库中 id=123,就把末 3 位 `112` 改成 `123`。⚠️ **切勿改变位数与格式** |
| C | Virtual Account Name | 持有人姓名 | 用户姓名 |
| D | Virtual Account IBAN | `AE270357414000620231020` | 必须**唯一**,建议用日期后缀避免重复;符合 UAE IBAN 结构(`AE` 起始) |
| E | Virtual Account Type | `Payment and Collection` | 表示同时支持付款与收款 |
| F | Hierarchy Type | `P` | 按模板示例维护 |

> 完整账户记录还含 Hierarchy Name、Email Address、Contact Number、Address line 1/2/3、Status(如 `Active`)、Approved/Rejected By、Approved/Rejected On 等字段(运营审批后回填),样例见原 wiki 归档;补录最小字段为上表 A–F。

## DB 校验点
- [[tbl_vis_t_virtual_account]](通过 `mid` 关联用户):
  - 申请激活落库后 `status = Initial`。
  - Job 批次处理调用 fab 成功后 `status = Valid`。
  - 库存不足时落库记录无 IBAN 信息。
- [[tbl_vis_t_notify_transaction_flow]]:Fitnesse 模拟交易通知后,交易流水落库此表。
- **IBAN 密文换算**:DB / Kibana 中 IBAN 等敏感字段以密文(持久令牌)存储时,用内部后台 PAYBY BASIS 的「带摘要持久令牌」工具做明文↔密文换算(Uat 入口 `https://uat.intra.test2pay.com/basis` → 综合管理 → 功能查询 → 加解密查询;数据类型选 `iban`,示例:明文 `AE27035741400060231020` + 摘要 `1020` → 密文形如 `P3194091-1020`)。

## 运营控台核对(Counter System → VIS Management)
运营侧用 Counter System(UAT:`uat.intra.test2pay.com/counter/`)核对 VIS 数据,VIS Management 子菜单:
- **File Flow**:VIS 相关文件流水。筛选 File ID / File Status / File Type / Date Range;右上 `Upload` 可上传结果文件。
  - 关键文件类型:`OF-开户申请文件`(状态 `Generated-已生成文件`)、`RF-开户结果文件`(开户结果回盘文件,解析成功后 Message `解析成功`、Status `Success`)。
  - 结果列:File ID | File Type | File Date | Status | Oss Path(如 `202310/counter/...openfile.xlsx`)| Message。
- **Virtual IBAN Account / Transaction Flow / Transaction Details / Statement Inquiry / Balance Inquiry / Vis Audit**:查询虚拟账户、交易流水与对账。

## 预期结果
- 激活成功 → 前端展示 IBAN 信息,DB `status=Valid`。
- 激活处理中 → DB `status=Initial`,等待 `vis_ibanAccountRetryJob` 重试转 `Valid`。
- 无库存 → DB 落库无 IBAN,前端无 IBAN 展示;人工补录后由 Job 重试转 `Valid`。
- VIP 用户走 Free Active(补姓名)激活;lean 用户绕过批次直接完成。
- Fitnesse 模拟交易通知后,流水落库 [[tbl_vis_t_notify_transaction_flow]]。

## 来源与置信
- 整理自归档 wiki/vam-iban(overview + 两份场景 + 导入模板 + 账户记录样例 + 激活/充值 UI + infra 访问的 IBAN 加解密部分)。
- 批次 Job 自动化对象、库存补录联系人为历史信息,标「待补 / 以实际为准」。
