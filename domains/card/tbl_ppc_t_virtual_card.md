---
id: tbl_ppc_t_virtual_card
object_type: Table
name: PPC 虚拟卡主表(t_virtual_card)
aliases: [t_virtual_card, virtual_card]
domain: card
status: active
owner: jianfei.wang
reviewer: jianfei.wang
last_reviewed_at: '2026-06-25'
source_type: wiki
source_ref: confluence:AQ/2133393518 + AQ/2133098640 (PPC 卡生命周期状态机 / 卡管理 API)
tags: [ppc, card, virtual-card, lifecycle]
related_services: [svc_ppc]
related_scenarios: [scn_card_lifecycle_transitions]
---

# PPC 虚拟卡主表(t_virtual_card)

## 用途
存储 PPC 预付卡(虚拟卡)的主记录与生命周期状态。卡的申请、激活、锁/解锁、关闭等所有状态流转都落在本表的 `status` 字段;PPC(svc_ppc)读写,卡管理 API(申请/激活/锁/解锁/关闭)在本表上完成状态机驱动。物理卡配送子状态与本表的虚拟卡状态**正交**(物理卡共用同一卡主体)。

## 关联关系
- **所属服务**:[[svc_ppc]](= frontmatter `related_services`,tbl→service 边)。卡核心 [[svc_cards]] 亦相关(绑卡/卡 token),具体读写边界待补。
- **谁读写它**:PPC 卡管理 API(申请/激活/锁/解锁/关闭/替换)、关卡静默批量任务(dormant cleanup)。
- **哪些场景校验它**:[[scn_card_lifecycle_transitions]](= `related_scenarios`)。

## 关键列
| 列 | 类型 | 说明 |
| --- | --- | --- |
| status | enum | 虚拟卡状态,取值见下方枚举(来源 `VirtualCardStatus.java`,提取自 ppc-SD-Manually Deactivate Card) |
| card_type / product_type | enum | 卡产品类型:MC=MULTI_CURRENCY(多币种卡)、PR=PAY_ROLL(工资卡);Salary Card 新增按 product_code 区分(SALCOB/SALMOB,见 [[reference_salary_card_cobadge]]) |
| (其余列) | - | 待补:原文未提供完整 DDL(卡号 proxy_no、member_id、余额、关卡订单字段等) |

### status 枚举
| Code | 名称 | 中文 | 最终态 | UI Summary Status |
| --- | --- | --- | --- | --- |
| A | APPLYING | 申请中 | 否 | PROCESSING |
| U | UNACTIVATED | 已发卡未激活 | 否 | UNACTIVATED |
| N | NORMAL | 正常/已激活 | 否 | NORMAL |
| L | LOCKED | 已锁定 | 否 | LOCKED |
| CI | CLOSING | 关卡中 | 否 | PROCESSING |
| C | CLOSED | 已关卡 | 是 | CLOSED |

> 待补:当前 enum 可能缺少 `APPLY_FAILED` / `DEACTIVATED` / `SUSPENDED` 等状态,需 PPC 后端确认完整 enum 与转换矩阵。

### 卡产品类型枚举
| Code | 名称 | 中文 | 允许的身份证件 |
| --- | --- | --- | --- |
| MC | MULTI_CURRENCY | 多币种卡 | EID, VIP_EID |
| PR | PAY_ROLL | 工资卡 | EID, PASSPORT, VIP_EID |

## 主键 / 索引
- 待补:原文未提供主键/索引定义。

## 校验点(QA 关注)
- 每次状态流转后 `status` 必须等于目标 enum 值(A/U/N/L/CI/C)。
- 关卡订单字段:FeeFlag=N, Flag=C, Amount=0(关卡时)。
- 申请失败后申请名额计数已释放。
- 销卡后(C)任何写操作不应改变本表对应行(资损红线)。
- 关卡前置:卡余额=0、待结算账户已清空、余额同步完成;否则返回 `NON_ZERO_BALANCE`。
- dormant cleanup 静默批量停用仅处理 MC 卡,PR 卡跳过。
