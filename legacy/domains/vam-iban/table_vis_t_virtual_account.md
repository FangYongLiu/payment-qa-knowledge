---
id: tbl_vis_t_virtual_account
object_type: Table
domain: vam-iban
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-19'
source_type: wiki_image
source_ref: wiki_image:346103a2-ffbf-43eb-b19b-eed5741c5414
tags:
- virtual-account
- iban
subdomain: null
module: null
sensitivity: normal
name: vis.t_virtual_account 虚拟账户表
aliases: []
related_services: []
related_tables: []
related_scenarios: []
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储用户 IBAN 虚拟账户信息。用户在 PayBy App 充值入口选择 Bank Account Transfer 并点击激活后,申请数据落地到本表,通过 `member_id`/`mid` 与用户关联。后续由 `vis_ibanAccountRetryJob` 批次处理(除 lean 场景外的 fab 用户申请),调用 fab 更新账户状态。申请成功后该行 `status=Valid` 且 `iban_no` 有值。

## 关键列
- `id`:记录主键(示例值 112)。
- `member_id`:用户标识,用于关联虚拟账户与用户。
- `hierarchy_name` / `hierarchy_type`:层级名称与类型(示例 `1` / `P`)。
- `file_id`:文件/批次标识(示例 `20231020000052502`)。
- `member_type`:会员类型(示例 `P`)。
- `name`:姓名字段(示例 `P3090095`)。
- `email` / `mobile_no`:联系方式(示例 email 为 NULL,mobile_no=`P2926593`)。
- `account_type`:账户类型(示例 `P&C`)。
- `address_country` / `address_city` / `address_details`:地址相关字段。
- `status`:账户状态。
  - `Initial`:申请落库后的初始状态(激活后未完成 fab 处理;包括 VIP 用户点击 Free Active 补充姓名后落库时也是 Initial)。
  - `Valid`:经 `vis_ibanAccountRetryJob` 批次触发并调用 fab 成功后更新为 Valid(成功示例值)。
- `request_type`:请求类型(示例 `A`)。
- `communicate_status`:与外部通讯状态(示例 `I`)。
- `message`:错误/响应信息(成功时为 NULL)。
- `extension`:扩展字段。
- `iban_no`:分配到的 IBAN 号(成功示例 `P3194091-1020`);IBAN 无库存时落库为空,需人工补充。
- `gmt_create` / `gmt_modified` / `gmt_complete`:创建/修改/完成时间。
- `notify_status`:通知状态(示例 `I`)。
- `maker_remarks` / `enrichment_field` / `primary_id` / `alias` / `parent_mapping`:补充与映射字段(示例均为 NULL)。

## 主键/索引
原文未明确给出索引;主键字段为 `id`(示例查询使用 `order by gmt_create desc`)。

## 校验点(QA 关注)
- 普通用户在 App 点击激活后,校验本表是否生成记录、`member_id` 是否正确关联、`status=Initial`。
- VIP 用户点击 Free Active 补充姓名信息时无前置校验,仍需确认数据落库且 `status=Initial`。
- 非 lean 场景的 fab 用户申请,需确认落库后由 `vis_ibanAccountRetryJob` 批次处理,job 触发后 `status` 由 `Initial` 更新为 `Valid`,且 `iban_no` 有值、`gmt_complete` 被填充。
- IBAN 库存为空场景:确认前端申请落库时 `iban_no` 为空,可人工补充 IBAN 数据后由 job 重试,最终 `status=Valid`。
- 申请成功记录示例字段组合可作为基线核对:`status=Valid`、`iban_no` 非空、`notify_status=I`、`communicate_status=I`、`message=NULL`、`gmt_complete` 非空。
- 配合 mock 配置 `vis.notification.mock=Y` 时不会调用 fab,需关注本表状态流转是否符合 mock 预期。
