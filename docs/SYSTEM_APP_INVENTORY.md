# 系统 APP 清单（权威源 · 282 个）

> 这是 PayBy 交易系统**全部 APP/服务模块的权威清单**（按管理后台页面顺序，282 个）。
> `scripts/import_services.py`（brain 仓）解析本文件，按 `gpXXX_/rtXXX_/bdXXX_/...` 前缀编号
> 分 `app_group`，为每个生成一个 Service 骨架对象到 `domains/_unassigned/`（待认领）。
> 架构图（`docs/system service map/SYSTEM_SERVICE_MAP.md` 的 ~40 个）只是其中一小部分，
> 已降级为「核心交易链路的边参考」，**不再当全集**。

## 第 1 页（1-20）
1. gp186_3ds2
2. gp275_acquire2-query
3. gp069_acquireii
4. gp008_acs
5. gp286_adg
6. gp125_adtaxi
7. rt002_afis
8. gp089_agreements-static
9. gp209_aml
10. gp225_asite
11. gp137_asset-info
12. rt005_at-beb
13. bd006_auth_server
14. gp060_authorization-service
15. gp101_authorization-token
16. gp034_authpay
17. gp274_bafl-channel
18. gp023_basis
19. gp300_basis-cas
20. gp094_basis-cms

## 第 2 页（21-40）
21. gp194_basis-customer
22. gp161_basis-merchant
23. gp295_basis-portal
24. gp038_bigdata-admin
25. gp268_bigdata-router
26. gp268_bigdata-router-admin
27. gp038_bigdata-ws
28. gp178_calculator
29. gp093_cards
30. gp058_cash-eatm
31. gp007_cashdesk-api
32. gp193_cashierii
33. gp081_cbm
34. gp086_cbs
35. gp180_cc-acquire
36. gp176_cc-cashier
37. gp159_cc-channel-btc
38. gp154_cc-channel-eth
39. gp181_cc-channel-tron
40. gp155_cc-deposit

## 第 3 页（41-60）
41. gp145_cc-sales
42. gp170_cc-trade
43. gp162_cc-transfer
44. gp146_cc-withdraw
45. gp140_ccdpm-accounting
46. gp140_ccdpm-manager
47. gp140_ccdpm-task
48. gp024_cgs
49. gt005_cgs-apitest
50. gp066_channel-mobile-ding
51. gp129_channel-paykii
52. op002_cicd
53. gp199_cloud-mis
54. gp002_cmf
55. gp002_cmf-task
56. gp091_cms
57. gp126_cmsii
58. gp289_cns
59. gp279_commission
60. gp160_comp-service

## 第 4 页（61-80）
61. gp107_contract
62. gp242_corporate-portal
63. gp031_counter
64. gp163_coupon
65. gp165_coupon-gateway
66. gp164_coupon-service
67. gp050_cps
68. gp080_cqm
69. bd006_crawl-leantech-server
70. bd006_crawl-server
71. gp130_credit-business
72. gp259_cregister
73. gp258_crs
74. gp138_crypto-currency-exchange
75. gp056_csc
76. gp070_csimple
77. gp096_css
78. gp136_custom
79. gp064_customer-frontend
80. gp278_customer-service

## 第 5 页（81-100）
81. gp207_das
82. gp204_data-etl
83. bd004_data-server
84. gp247_datasavvy
85. gp205_deduct
86. gp011_deposit
87. gp054_device
88. gp184_df-calculation
89. gp004_dpm-accounting
90. gp004_dpm-manager
91. gp004_dpm-task
92. gp020_dubbo-admin
93. gp021_elasticjob-console
94. gp104_escrow
95. gp231_escrowii
96. gp156_exchange
97. gp294_exchange-rate-crawler
98. gp139_facepay-api
99. gp039_fcw
100. bd007_feature-calculate-server

## 第 6 页（101-120）
101. bd007_feature-calculate-server-new
102. gp239_feebill
103. gp057_fido-mgmt
104. gp057_fidoservice
105. gp192_fraud
106. gp318_fundchannel-mock
107. gp012_fundout
108. gp185_gadget
109. gp302_gold-wallet
110. gp099_gpoint
111. gp296_gppc
112. gp297_gppc-jaywan
113. gp110_gptrade
114. gp079_grc-check-identity-provider
115. gp079_grc-component-connect-provider
116. gp079_grc-cps-provider
117. gp079_grc-engine-provider
118. gp098_green-points
119. gp062_h2h
120. gp048_hive-activities

## 第 7 页（121-140）
121. gp048_hive-bank-console
122. gp048_hive-cashier
123. gp048_hive-checkout
124. gp048_hive-developers
125. gp048_hive-m-topay
126. gp048_hive-mcashier
127. gp048_hive-merchant-console
128. gp048_hive-portal
129. gp048_hive-utilities
130. gp144_holding
131. gp150_host
132. gp151_host-gateway
133. gp240_household
134. gp238_ifb-channel
135. gp122_invoice
136. gp106_iso8583-gateway
137. gp997_jollychic-service
138. gp103_kiosk-channel
139. rt006_kiosk-mgmt
140. gp078_kyc

## 第 8 页（141-160）
141. gp202_kyc-service
142. gp233_leanlink
143. gp074_life-center
144. gp075_market-goods
145. gp076_market-order
146. gp068_marketing
147. gp189_marketing-campaign
148. gp105_marketing-event
149. gp190_marketing-gateway
150. gp131_marketnotify
151. gp127_mcs
152. gp005_member
153. gp148_member-feature
154. gp135_member-front
155. gp270_member-task
156. gp044_merchant
157. gp045_merchant-console-frontend
158. gp071_merchant-frontend
159. gp083_merchant-fundout
160. gp288_merchant-settlement

## 第 9 页（161-180）
161. gp037_mns-listener
162. gp037_mns-main
163. gp037_mns-scheduler
164. gp243_mock-channel
165. gp223_mock-datawire
166. gp990_mock-ni
167. gp141_mssii
168. bd002_mysql-member-sync
169. gp280_ni-mock
170. gp222_npss
171. gp210_npss-gateway
172. gp085_oauth-client-service-cgs-impl
173. gp281_officer
174. gp308_offline-payment
175. gp254_onboarding
176. gp100_ons
177. gp084_otpmock
178. gp084_otps
179. gp016_outman
180. rt004_palm-id

## 第 10 页（181-200）
181. gp095_paylater
182. gp006_payment
183. gp237_payroll-core-service
184. gp003_pbs
185. gp041_pbs-bos
186. gp283_pcbs
187. gp046_pcm
188. gp042_pcs
189. gp032_personal
190. gp014_pfs-basis
191. gp014_pfs-manager
192. gp014_pfs-payment
193. gp261_pix
194. gp013_pns
195. gp304_pns-merchant-mocker
196. gp065_porter
197. gp213_pos-exception-processor
198. gp026_pos-gateway
199. gp212_ppc
200. gp047_ppcenter

## 第 11 页（201-220）
201. rt003_pqs
202. gp197_preauth
203. rt001_promo-campaign
204. rt001_promo-engine
205. rt001_promo-gateway
206. rt001_promo-merchant
207. gp120_protocol
208. gp120_protocol-duplicate
209. gp040_pts
210. gp230_pus
211. gp227_push-to-pay
212. gp284_pws
213. gp232_qpay-aplus
214. gp221_qpay-cko
215. gp269_qpay-enbd
216. gp088_qpay-fs
217. gp200_qpay-fsii
218. gp245_qpay-fts
219. gp158_qpay-installment
220. gp201_qpay-klip

## 第 12 页（221-240）
221. gp234_qpay-lean
222. gp087_qpay-mcii
223. gp267_qpay-mpgs
224. gp187_qpay-ni-channel
225. gp262_qpay-niboarding
226. gp244_qpay-nipos
227. gp252_qpay-nisocket
228. gp301_qpay-npss
229. gp092_qpay-pl-channel
230. gp313_qpay-zand
231. gp030_query
232. gp030_query-datasync
233. gp142_quotation
234. gp216_rdgs
235. gp043_reconciliation
236. gp188_remittance
237. gp264_remittance-bdo
238. gp307_remittance-cbe
239. gp303_remittance-codepoint
240. gp287_remittance-ext

## 第 13 页（241-260）
241. gp299_remittance-fawry
242. gp290_remittance-fuze
243. gp276_remittance-ime
244. gp312_remittance-jinglepay
245. gp293_remittance-platon
246. gp257_remittance-swiftx
247. gp298_remittance-trustbank
248. gp085_resource-service-cgs-impl
249. gp085_resource-service-rpc-dubbo-provider
250. gp085_resource-service-sgs-impl
251. gp085_resource-service-web
252. gp124_router
253. gp291_rtp
254. gp085_session-service-cgs-impl
255. gp085_session-service-rpc-dubbo-provider
256. gp028_sgs
257. gp116_shortlink
258. gp035_socialpay
259. gp022_software-management
260. gp018_spring-boot-admin

## 第 14 页（261-280）
261. gp019_spring-cloud-config
262. gp055_sqlmonitor
263. gp134_statementii
264. gp073_supplier
265. gp292_tld-service
266. gp195_tpay-nyu
267. gp123_tradeii
268. gp053_transfer
269. gp311_tts
270. bd004_uae-data-server
271. gp001_ues-ws
272. gp114_ufs2
273. gp251_unified-merchant-portal
274. gp153_upic
275. gp077_user-profile-scheduler
276. gp133_vcs
277. gp149_vis
278. gp317_visii
279. gp009_voucher
280. gp236_wechat-channel

## 第 15 页（281-282）
281. gp033_xbh-gateway
282. gp220_youstore-installment
