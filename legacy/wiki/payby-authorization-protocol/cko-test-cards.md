---
title: CKO测试卡号清单
domain: authorization-protocol
kind: wiki_page
slug: cko-test-cards
status: archived
owner: upload-sync@platform
reviewer: UNREVIEWED
source_type: wiki
source_ref: wiki:9770c9b6-cd5c-4f9d-ae94-6d4e4b107220
tags: []
---

# CKO测试卡号清单

本页汇总 CKO 渠道联调/测试时常用的测试卡号，覆盖本地卡、外卡及鉴权失败场景。

## 测试卡号

| 卡号 | 说明 |
| --- | --- |
| 4010 0617 0000 0021 | 本地卡 - Debit |
| 5385 3083 6013 5181 | 本地卡 - Credit |
| 4659 1055 6905 1157 | 外卡 - Debit |
| 4242 4242 4242 4242 | 外卡 - Credit |
| 4870 5270 1770 0692 | Authentication rejected（鉴权拒绝） |

## 参考链接

- Checkout 官方测试卡文档：https://www.checkout.com/docs/developer-resources/testing/test-cards

## 相关场景

- 卡号可用于 [[scn_cko_standalone_card_binding]]，绑卡成功后 token 会落地至 [[tbl_member_tr_bank_card_token]]。
- 整体方案参见 [[cko-channel-subscription-payment]]。
