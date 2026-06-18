---
id: tbl_fiserv_ping_url
object_type: Table
domain: payby-authorization-protocol
status: active
owner: wiki-sync@acquire
reviewer: UNREVIEWED
last_reviewed_at: '2026-06-18'
source_type: wiki
source_ref: confluence:AQ/2199912473
tags:
- fiserv
- routing
- ping
subdomain: fiserv
module: qpay-fsii
sensitivity: normal
name: fiserv.t_ping_url
aliases: []
related_services: []
related_tables:
- tbl_fiserv_out_bound
related_scenarios:
- scn_fiserv_test_tid_creation
related_logs: []
related_requirements: []
related_failures: []
---

## 用途
存储 qpay-fsii 在 Fiserv 渠道绑定阶段从 register_url 注册后获得的 4 个 ping_url，以及对每个 URL 进行 ping 探测得到的响应耗时 (response_time_ms)。

在交易阶段，qpay-fsii 收到交易请求后，从该表中挑选 response_time_ms 最小（速度最快）的 ping_url，向其发送交易报文，用于路由选路。

## 关键列
- ping_url：注册阶段返回的 4 个 URL 之一，用于发送交易报文。
- response_time_ms：对该 ping_url 进行 ping 测试的响应耗时，作为选路依据（取最小值）。
- update_time：记录该 ping_url 数据的更新时间，用于判断有效期。

## 主键/索引
原文未明确说明主键/索引定义。

## 校验点(QA 关注)
- 渠道绑定成功后，应在该表中落 4 条 ping_url 记录，且每条都有可用的 response_time_ms。
- Fiserv 要求每 6 小时重新获取一次 ping_url：系统只把 update_time 在最近 6 小时之内的 URL 视为有效的 ping_url。需校验过期数据不会被用于交易选路。
- 交易时选路逻辑：从该表中筛选有效记录后，选择 response_time_ms 最小的 url 发送交易报文。
- 与 fiserv.t_registration、fiserv.t_reg_url 的关联：ping_url 来源于 register_url 的注册返回结果。

================================================================================

# 文档 28: payby-authorization-protocol/scn_fiserv_test_tid_creation.md

================================================================================

# Conversation: payby-authorization-protocol/scn_fiserv_test_tid_creation.md

Generated: 2025-11-13T08:13:35.124Z

---

## 👤 User

你是资深支付 QA，把文档里某个技术对象整理成结构化知识对象。先输出元数据 JSON，再输出正文 markdown——正文绝不放进 JSON(避免转义/截断)。

---

## 🤖 Claude

理解。请提供文档内容和需要整理的技术对象信息，我将按照以下格式输出：

1. **元数据 JSON**（单独代码块）
2. **正文 Markdown**（单独代码块）

请发送：
- 原始文档内容
- 目标技术对象的名称/范围（如某个接口、表、字段、状态机、错误码等）
- 如有特定的 schema 要求（字段定义），请一并提供；否则我将使用通用结构：

```json
{
  "id": "对象唯一标识",
  "type": "API|Table|Field|StateMachine|ErrorCode|Flow|Component|...",
  "name": "对象名称",
  "domain": "所属业务域",
  "summary": "一句话摘要",
  "tags": ["标签"],
  "source": {
    "doc": "文档名",
    "section": "章节定位"
  },
  "related": ["关联对象id"],
  "version": "版本/更新时间"
}
```

请提供材料。

---

## 👤 User

根据【整篇原文】，把对象 id=scn_fiserv_test_tid_creation (Scenario, name=测试环境构造Fiserv TID) 整理出来。

第一部分：输出元数据 JSON(单行紧凑，**不含正文**)：
{"id":"scn_fiserv_test_tid_creation","object_type":"Scenario","domain":"payby-authorization-protocol","name":"测试环境构造Fiserv TID",
"aliases":[],"tags":[],"subdomain":null,"module":null,
"related_services":[],"related_tables":[],"related_scenarios":[],"related_logs":[],"related_failures":[]}
(subdomain/module 可选，无合适值留 null；related_* 用真实 id，无则留空数组——优先取自【可链接清单】)

第二部分：单独一行写 `===BODY===`，然后输出正文 markdown，按此骨架：
## 场景目的
## 前置条件
## 操作步骤
## 校验点

正文要求：忠实且精炼(字段名/表名/错误码/状态/路径原样保留，不改写专有名词)；只写属于
本对象 scope=在测试环境手动构造可绑定的TID数据 的内容；原文没有的不编造。

【可链接清单】
- [[fiserv-channel-binding-and-payment]] Fiserv渠道绑定与支付流程
- [[flow_fiserv_channel_binding]] (Flow) Fiserv渠道绑定流程
- [[flow_fiserv_pos_payment]] (Flow) Fiserv POS刷卡交易流程
- [[tbl_fiserv_out_bound]] (Table) device.t_fiserv_out_bound
- [[tbl_fiserv_ping_url]] (Table) fiserv.t_ping_url
- [[scn_fiserv_test_tid_creation]] (Scenario) 测试环境构造Fiserv TID

【整篇原文】
流程：
Fiserv提供outbound文件(原始文件是.xml格式)到sftp
PayBy每天扫描sftp文件并解析为excel格式文件保存到我们系统，解析后的数据落库：
device.t_fiserv_out_bound where config_status='INACTIVE'
设备扫码激活
在basis merchant → TMS → Activated Devices → Fiserv Outbound Files目录中可以查看解析到的所有的TID数据
设备绑定渠道TID： basis merchant → TMS → Activated Devices → Activated Devices, Device Configuration, 输入在Fiserv Outbound Files中状态为Inactive的TID
测试环境怎么创造新的TID：
device.t_fiserv_out_bound 中手动插入config_status='INACTIVE'的数据，文件路径不重要，重要的是TID不能重复，mid分两种：1209开头（出租车公司的）和7600（非出租车公司）的，store_id（如果mid是1209开头，那就是把mid的前2位换成8116，作为store_id填进来；如果mid是7600开头，那就是把mid的前4位换成8116，作为store_id填进来)
测试环境怎么绑定渠道
测试环境可以链接Fiserv，但是Fiserv的测试环境不止给我们用，他们给我们的TID有时会改配置导致交易失败。所以我们一般用mock
绑定的逻辑：
配置用来做sever discovery的datewire url在qpay-fsii配置文件中
绑定的时候先请求server discovery做服务发现(这个注册请求保存在
fiserv.t_registration
)，得到register_url(保存在
fiserv.t_reg_url
)，这个是用来注册TID的
然后qpay-fsii请求register_url去注册，得到4个ping_url
qpay-fs
