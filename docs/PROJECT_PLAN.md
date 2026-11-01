# 第28组区块链托管应用大作业执行计划

## 目标与完成标准

组长武钰斐（202492451119）；主力开发武钰斐、苏佳豪；杨燊杰承担少量实际角色验收及记录任务。该分工是待执行安排，完成后以提交记录、真实操作和证据确认，不预先记为已完成贡献。

选择路线B为必做，完整路线A为加分，并完成重入攻击及修复、订单时间线、发货状态、两人一致的多签仲裁。五项名义合计21分，暂按07专门评分文件最多计20分，总成绩封顶100分；04讲义“最多10分”与07冲突，提交前确认教师最终口径，实施范围仍覆盖全部五项。目标是覆盖全部评分点，不承诺教师评分或答辩必得满分。

用户已确认2026年11月8日截止，具体时刻待确认。自11月1日起安排7天，11月7日晚完成内部交付，11月8日预留提交缓冲。两名主力各每天约3—5小时，11月5—7日另留2小时机动；以各阶段出口条件核对进度，不把估算当已完成工作。

交付：可访问Git仓库、两条完整路线、扩展合约与页面、攻击/修复演示、自动化测试、真实交易台账、全部截图与解释、README、真实分工表、包含独立“AI使用说明”的报告及答辩材料。

## 2026年11月1日实际基线

- GitHub已核实仓库存在，检查时只有README和初始提交`2752218ef2dbd7c8baa848ea2c0f8890a6bd06c5`，尚无作业代码；该初始提交时间为10月26日。建库不等于功能已完成。
- 用户本次明确同意将仓库公开，供苏佳豪直接fork；苏的用户名不再是开工前置条件。本轮同步规划文档，代码导入仍为T01待执行内容。
- 两个旧WSL工程均存在，Escrow.sol、WYFToken.sol、Escrow.ts和构建配置已核对；两个旧目录都不是Git仓库。规划的新协作目录尚不存在。保留新仓库的现有历史，再导入筛选后的源文件。
- 原部署地址、成员钱包归属和测试网余额来自前次计划，本轮未重新查询链上数据；T02及角色预约完成前，不声称已复核。
- 班级、统一报告模板与11月8日的具体截止时刻待补；不阻塞开发，模板最迟11月3日取得。

## 已核实的工程与参考

- 本地前端工程：`/home/wuyufei/blockchain-course/my-first-dapp`，现有 `packages/hardhat/contracts/Escrow.sol`、`WYFToken.sol`、`test/Escrow.ts` 与Scaffold hooks均存在。
- 本地Java示例：`/home/wuyufei/blockchain-course/spring-boot-web3j`，Java21、Spring Boot3.2.3、Web3j4.14.0、Gradle8.13；当前无已核实的Java测试覆盖，需补测试依赖。
- 前端继续使用现有Yarn3.2.3与锁文件，Node须满足`>=20.18.3`；不在本作业顺便升级Next/React/Wagmi/Viem。
- 现有Hardhat脚本的测试网络明确为`hardhat`；本地部署必须显式`--network localhost`，POTOS部署必须显式`--network potos_testnet`。不使用省略网络的部署命令。
- 本地与上游相同的`writeContractAsync`经`useTransactor`等待成功回执后才返回hash；仍需处理`undefined`、用户拒签、回退、超时、替换。直接wagmi写入或其他封装须单独核实回执语义。
- 现有事件hook历史批量默认500、实时分支没有复用10块分段；课程RPC要求小区间扫描，必须覆盖初始与断线后的追赶。
- 本次规划复核：Metis预设代理因模型不可用未运行，已由可用的只读代理完成缺口复核；纳入了日期、fork流程、真实基线、AI说明、角色预约及BE隔离等修正。该复核不代表实现或测试已通过。

官方示例固定版本参考：

1. Frontend `a8436fde196c3b64a42bf75413f1083e901f1927`：https://github.com/kyonRay/my-first-dapp/tree/a8436fde196c3b64a42bf75413f1083e901f1927
2. Java `a36f03e5c26a9df77dd6acc17c4b1a4eef6616af`：https://github.com/kyonRay/spring-boot-web3j/tree/a36f03e5c26a9df77dd6acc17c4b1a4eef6616af
3. 回执等待：https://github.com/kyonRay/my-first-dapp/blob/a8436fde196c3b64a42bf75413f1083e901f1927/packages/nextjs/hooks/scaffold-eth/useTransactor.tsx#L60-L111
4. 事件历史与实时分支：https://github.com/kyonRay/my-first-dapp/blob/a8436fde196c3b64a42bf75413f1083e901f1927/packages/nextjs/hooks/scaffold-eth/useScaffoldEventHistory.ts#L128-L291
5. Java构建：https://github.com/kyonRay/spring-boot-web3j/blob/a36f03e5c26a9df77dd6acc17c4b1a4eef6616af/build.gradle

课程依据：本机`04-大作业-在区块链上构建应用系统.pdf`第1—19页，`07-大作业任务书及评分标准.pdf`第1—3页；目录为`D:/WeChat/xwechat_files/wxid_bil0990tqje722_041e/msg/file/2026-10/`。

## 协作仓库与文件归属

仓库：https://github.com/wuyufei0817/blockchain-escrow-group28 ；账号`wuyufei0817`。用户已授权公开。武钰斐维护主仓库；苏佳豪从网页Fork到本人账号后开发，通过PR合回武的`main`，无需先邀请为协作者。

苏佳豪本机`origin`指向个人fork，`upstream`指向武的主仓库。首次clone自己的fork后执行：

```bash
git remote add upstream https://github.com/wuyufei0817/blockchain-escrow-group28.git
git fetch upstream
git switch -c feat/su-backend upstream/main
```

每天开始前拉取`upstream/main`，在干净工作区将其合入本人功能分支，解决冲突后继续；push到本人`origin`，PR目标选`wuyufei0817/blockchain-escrow-group28:main`。武合并后，苏同步fork再开展下一任务。先完成T01代码基线；提前fork也可以，但开始开发前必须同步代码基线。依据：[GitHub fork协作说明](https://docs.github.com/en/pull-requests/how-tos/work-with-forks/fork-a-repo)。

新的工作目录定为`/home/wuyufei/blockchain-course/blockchain-escrow-group28`；原实验目录保留。导入清理过的源文件和锁文件，不迁移旧`.git`、钱包、私钥、`.env`、构建缓存。仓库根沿用Yarn工作区结构，Java放`backend/`。

| 人员 | 主要责任与独占修改范围 | 验收/报告责任 |
|---|---|---|
| 武钰斐 | `packages/nextjs/app/escrow/`、`app/escrow-plus/`、`components/escrow/`、`hooks/escrow/`、`utils/escrow/`；`EscrowPlus.sol`、`EscrowPlus.ts`、扩展部署；根配置与集成 | 组长；B路线与发货/多签演示；总台账、报告整合、发布检查 |
| 苏佳豪 | `backend/**`；`VulnerableVault.sol`、`FixedVault.sol`、`Attacker.sol`及对应测试和部署；不改武钰斐页面/扩展合约 | A路线全部接口与解释；重入挑战；复核B、测试网回执与金额 |
| 杨燊杰 | 不安排主要编码；实际执行本人钱包的卖家争议/发货等验收操作，核对截图和记录 | 小规模真实贡献：角色截图、验收记录、报告一致性核对；实际未做的事项不填为已完成 |

共享文件`package.json`、`yarn.lock`、`hardhat.config.ts`、生成ABI配置和README由武钰斐合并；苏需要变更时在PR说明，由组长整合。分支：`feat/wu-escrow-ui`、`feat/wu-escrow-plus`、`feat/su-backend`、`feat/su-reentrancy`；`main`只保留通过检查的提交。每次PR描述功能、测试、证据位置及本人贡献。

若杨不能实际参与，不能宣称三人已完成；须按事实记录两人工作，并就三角色页面验收方式向助教确认。不能通过两人代签后写成第三人操作满足分工。

## 合约和账户边界

| 别名 | 用途 | 实例与签名 |
|---|---|---|
| B_BASE | 必做B，完全保留实验3原ABI/状态机 | chain60600；Escrow `0xbdB2Dfcd8A9Cd903848a1B9d95416b85178f05Af`；token `0x81777CEeA8CC59fa88ABcee9DC19970217Cf8637`；买家武、卖家杨、仲裁苏 |
| A_BASE | 完整加分A | 新部署原Escrow；仲裁人是苏本机持有的新后端专用钱包BE；买卖双方仍用各自MetaMask |
| PLUS | 发货与两人一致仲裁 | 新部署`EscrowPlus`；MS1由苏、MS2由武各自创建并在本人浏览器钱包持有；两地址不同，均不同于A后端专用BE；两个不同地址均须真实上链投票 |
| VULN / FIXED | 仅本组测试币重入实验 | 两份金库、分别绑定的Attacker；与托管业务资金完全分开登记 |

历史B_BASE已有订单0—3。新验收必须读取`OrderCreated`回执确定真实ID，以`B-NORMAL`/`B-DISPUTE`标识业务用途，不能把真实ID4、5等改写为0、1。A_BASE全新部署的初始ID通常为0、1，也须核对事件。新部署区块必须从回执取得，不能猜测或从0扫描全链。

保留Created0、Paid1、Completed2、Refunded3、Disputed4；PLUS把Shipped追加为5。原Escrow.sol不为加分更改；PLUS不能代替基础路线验收。

私钥仅本机环境变量或用户自持钱包使用，不在聊天、截图、仓库和PR中出现。`WEB3J_PRIVATE_KEY`仅给A后端，PLUS不复用该账户；前端只连接MS1/MS2等用户钱包，无私钥。`NEXT_PUBLIC_`变量只能放公开RPC/链信息。链上签名由账户本人完成，代理可自动化本地测试和只读回执核验。

## 加分与证据矩阵

| 项目 | 分值 | 必须完成的行为 | 独立证据 |
|---|---:|---|---|
| B基础 | 40+40相关 | 列表/创建/两笔付款/确认/争议/仲裁/角色7功能 | 4B-1—4B-6，4B-1—4B-5解释，真实B交易台账 |
| A完整路线 | +6 | 原6接口、Java封装、SimpleStorage、后端仲裁、错误状态仲裁真实失败 | 4A-1—4A-8及6题解释；A独立地址/账户/台账 |
| 重入复现与修复 | +6 | 漏洞金库被本组Attacker提走本组受害者测试币，修复后相同攻击失败 | 4C-1—4C-3；两轮余额、hash、失败status与本地测试 |
| 时间线 | +3 | A新增events接口；B订单展开呈现全部适用事件且排序正确 | `BONUS-TIMELINE`截图、响应与跨10块/断线追赶测试 |
| Shipped | +3 | 卖家Paid发货；已发货不得普通超期退款；测试、页面同步 | `BONUS-SHIPPED`发货、受限退款、正常确认/争议证据 |
| 两人一致仲裁 | +3 | 两个不同msg.sender均真实resolve且意见一致后才转账 | `BONUS-MULTISIG`第一票/不一致/达成一致/防重复的回执与余额 |

报告首页写仓库URL、真实分工及负责文件；README和报告均列全8个规定操作，另附双路线及加分交易。A作为八行完整主台账：部署、createOrder正常单、approve、deposit正常单、dispute争议单、resolve争议单、confirm正常单、resolve未争议正常单失败；另记录第二笔create/deposit等，不能遗漏或用不适用占位。B单独记录对应全部真实操作与已有部署交易，不能混用A/B哈希。

台账字段：路线/合约别名、业务标签、真实orderId、操作、完整hash、区块号、from、to、receipt status、gasUsed、浏览器链接。数量与状态均取实际读数，未上链的模拟失败没有hash，不伪造填入。

## 执行波次与时间安排

| 日期 | 武钰斐当天交付 | 苏佳豪当天交付 | 当天验收与关口 |
|---|---|---|---|
| 11月1日 | T01清理导入与首次可构建提交，T02地址/ABI/证据约定 | fork、同步代码、验证Java环境，确认六接口字段 | 预约杨的卖家操作；核实原arbiter可由苏本人签名；记录初始余额；两人均可运行基线 |
| 11月2日 | T03/T04：订单列表、创建、连续付款 | T07/T08：Java封装、示例、六接口及失败响应 | B本地Created->Paid；A的SimpleStorage=100、六接口本地可调用 |
| 11月3日 | T05：角色权限和基础动作，补本地反例 | T09：事件列表/时间线；完成A本地联调 | 基础代码完成；25块跨段索引测试通过；报告模板取得；预约11月4日三角色会话 |
| 11月4日 | T06：B测试网完整业务流和4B截图/解释草稿 | T10：A测试网完整业务流和4A截图/解释草稿 | 两路线真实回执核对，打`baseline-complete`；杨实际执行卖家步骤。此日前若基础未通过，5日先补基础并报告实际进度 |
| 11月5日 | T11/T12：Shipped和双人仲裁合约、正反测试 | T14：漏洞/修复/Attacker及资金断言；整理A时间线证据 | 扩展本地通过；A/B时间线各有证据；确认PLUS的MS1/MS2，预约6日共同测试 |
| 11月6日 | T13：PLUS页面、发货/超时退款限制/两人一致裁决 | T15：测试网两轮重入演示和4C证据；本人用MS1投票 | 五项加分全部逐项核验，包含两人分歧不转账和修复后攻击失败；当天修完功能问题 |
| 11月7日 | T16：合并报告、八行台账、分工、AI说明与提交包 | 干净clone按README运行前端，核对哈希和金额；双方交叉讲解 | 19:00前冻结功能，21:00前完成内部交付；杨完成本人截图/记录和说明复核；留出答辩演练 |
| 11月8日 | 最终核查文件名、首页仓库链接和附件，组长提交 | 复核提交版与仓库版本一致，保留备份 | 按教师明确时刻提交；在未知具体时刻时不拖到晚间。本轮不代发邮件 |

表中时间是内部目标，不是教师给出的时限。每天结束用“可演示结果＋测试输出＋截图/回执”更新任务状态；正文后续D0—D6为逻辑阶段，实际日期以上表为准。

### 第一轮开工顺序（11月1日，约3—5小时）

1. 武核对仓库README与最新提交，在WSL新目录clone主仓库；苏先核对JDK21和Gradle环境。
2. 武从两个旧目录筛选导入源码与锁文件，Java放`backend/`，保留LICENSE，处理示例私钥与忽略规则；此时不部署新合约。
3. 武执行安装/编译/已有测试，苏验证Java wrapper生成；出现环境问题先解决，未通过不标记基线完成。
4. 武提交代码基线；苏fork或同步已有fork，再clone并配置`upstream`，提交一个本人真实完成的README环境核对小PR，以验证协作流程。
5. 共同冻结T02接口/状态/金额/地址格式，核实B_BASE的arbiter和钱包角色；最迟当晚确认杨能在4日参加卖家步骤、6日参加发货步骤、7日整理记录。若不能参加，立即调整真实贡献安排和三人验收方式。
6. 从当天起维护`docs/ai-usage-log.md`：工具、用途、建议、发现的问题、验证/修正及责任人。记录真实发生的案例，不编造AI错误。

| 阶段 | 武钰斐 | 苏佳豪 | 杨燊杰/共同验收 | 出口条件 |
|---|---|---|---|---|
| D0 准备 | T01、T02，仓库与接口冻结 | 本机JDK/Gradle/后端环境核对 | 确认能参与的时间 | 无密钥导入仓库；两机可运行 |
| D1—D2 基础并行 | T03、T04、T05，B页面 | T07、T08、T09，A接口 | 按角色准备钱包 | 本地测试、编译、类型检查通过 |
| D3 基础冻结 | T06真实B流程 | T10真实A流程 | 页面卖家操作及截图 | A/B必做截图和解释全部可核查，打`baseline-complete`标签 |
| D4—D5 加分并行 | T11、T12、T13 | T14、T15 | 扩展卖家发货/争议 | 五项加分均有独立成功与失败证据 |
| D6 集成交付 | T16，报告与发布 | 交叉验证README/交易/解释 | 完成本人实际记录 | 测试通过、仓库可访问、报告无占位、答辩演练完成 |

每天结束合并已验收的可演示增量；先保基础，再完成全部加分。11月4日基础关口或11月6日全加分关口滑期时，当晚列出缺口、剩余工时和两人第二天的具体补救安排，及时压缩样式与可选优化，不缩减要求的功能/证据，也不把未验证项目写为完成。

## 验证策略

合约采用测试先行：原8项回归继续保留，新增加分的状态/权限/资金/意见冲突等每条规则都有正反例。Java增加Spring Boot测试依赖，Controller/Service用JUnit5与Mockito隔离RPC，并在本地Hardhat做接口集成。前端先类型检查与构建，再由真实钱包按场景验收，不用仅mock钱包的测试代替测试网记录。

基本检查命令（新仓库根）：`yarn install --immutable`、`yarn compile`、`yarn hardhat:test`、`yarn next:check-types`、`yarn next:build`；Java在`backend/`执行`bash gradlew generateContractWrappers test bootJar`。新增无密钥扫描命令为`node scripts/verify-no-secrets.mjs`，须在T01实现后才使用，不宣称当前已存在。

证据目录：`docs/evidence/A/`、`B/`、`C/`、`bonuses/`，原始图片不改字、不拼接；每项附说明：操作者/角色/链/地址/orderId/hash/预期与实际。`.omo/evidence/`放本地自动测试输出。原始失败原因、HTTP失败、模拟失败、已上链回退分别记录。

## 任务依赖

| 任务 | 依赖 | 负责人 |
|---|---|---|
| T01 | 无 | 武 |
| T02 | T01 | 武+苏确认 |
| T03 | T02 | 武 |
| T04 | T02 | 武 |
| T05 | T03、T04 | 武 |
| T06 | T03、T04、T05 | 武领衔，三角色 |
| T07 | T01、T02 | 苏 |
| T08 | T07 | 苏 |
| T09 | T07、T02 | 苏 |
| T10 | T08、T09 | 苏领衔，买卖家配合 |
| T11 | T06、T10基础冻结 | 武 |
| T12 | T11 | 武 |
| T13 | T03、T11、T12 | 武 |
| T14 | T01 | 苏，可与基础开发并行但不拖基础 |
| T15 | T14、基础冻结 | 苏领衔，武提供受害者账户操作 |
| T16 | T06、T10、T13、T15 | 武整合，苏复核，杨记录 |

## TODO任务明细

- [ ] T01 协作基线与安全导入（武钰斐）

  **执行**：新目录clone已公开的主仓库，保留现有Git历史；以清理过的源码导入现有Yarn项目和`backend/`，保留上游LICENSE；旧目录非Git仓库，不迁移钱包/环境文件。清除Hardhat、Java配置及示例README中的示例私钥和敏感默认回退。增加`.env.example`空占位、忽略规则、`scripts/verify-no-secrets.mjs`及`docs/ai-usage-log.md`；本地/测试网显式区分31337/60600。现有实验工程不改动。
  **参考**：已存在两个本地工程的package.json、build.gradle；官方Java配置及Hardhat配置；04第4.2/7.2节。新脚本和`backend/`是本任务新增。
  **验收**：干净clone能安装；`yarn install --immutable`与Java编译可用；扫描工作树与Git历史没有明文密钥。64位hex须分类：真实交易hash/区块hash/topic/生成bytecode不是私钥，不能为通过扫描删除必需台账或BINARY。扫描仅报路径/行号/类型，不输出秘密值。
  **QA 正常**：两人独立clone，记录版本与启动命令，证据`.omo/evidence/T01-clean-clone.txt`。
  **QA 失败**：在临时未跟踪fixture写入测试用伪密钥赋值，扫描应失败且不打印值；公开hash fixture应通过，删除fixture后再提交。
  **提交**：`chore: establish sanitized capstone workspace`。依赖无；解锁T02、T07、T14。

- [ ] T02 注册表、契约与台账冻结（武钰斐，苏确认）

  **执行**：新增`docs/deployments.json`、`docs/api-contract.md`、`docs/transactions.md`、`docs/evidence/manifest.md`。登记B_BASE原地址、ABI来源、真实部署区块及chain60600；校验代码非空、WYF精度18、owner/arbiter；读当前orderCount和余额。A/PLUS/Vault部署后逐条补实际数据，未部署不填假地址。明确整数在JSON中用十进制字符串，状态文字及ISO/秒单位；所有UI统一钱包地址大小写归一比较。
  **参考**：原Escrow/WYF源码及部署记录、04第7.1节；B_BASE原部署hash `0x7cb22a0da3735a5caed06db50f7c048703ca5e8468baca998b09d9e52a3288dc`，执行前查询其回执得到真实区块。
  **验收**：注册表不混入实验2 token `0xc240...`或其他组员合约；两开发者确认相同ABI/字段/URL；主台账八行有固定操作定义和待捕获状态。
  **QA 正常**：只读chainId、code、arbiter、decimals与登记一致；证据`T02-registry.json`。
  **QA 失败**：连接31337或无代码地址时禁止测试网写入并显示明确错误，不自动改用另一合约。
  **提交**：`docs: freeze contracts and evidence conventions`。依赖T01。

- [ ] T03 B订单索引、列表与时间线（武钰斐）

  **执行**：新增`app/escrow/page.tsx`、组件`OrderList/OrderTimeline`、`hooks/escrow/useEscrowIndex.ts`、`utils/escrow/logRanges.ts`等小模块。决定采用独立轻量索引适配器，保留原框架hook不改：address限定Escrow，原始`eth_getLogs`显式`topics:[]`，每段最多10块，解码该地址全部已知订单事件；Created发现订单ID，当前状态由getOrder读取，时间线按blockNumber/transactionIndex/logIndex升序。初始与实时缺口使用同一分段器；每批成功后持久化checkpoint，缓存key含chain/address/deployBlock，按blockHash/txHash/logIndex去重；展示进度、失败重试和最新同步块。时间线按订单懒展开，UI列表分页与RPC区块分段独立。
  **参考**：现有`useScaffoldEventHistory.ts`历史和实时分支、原六类事件；04第5.1、5.2、6节。
  **验收**：不用orderCount循环作为列表发现来源；不从0扫链；完整扫描稳定头后Created数量与orderCount交叉核对，若10块请求仍疑似漏日志，重扫问题范围为1块/请求并报告，不静默宣称完整。只读重试有界退避、并发最多2；交易发送不套用自动重试。
  **QA 正常**：本地订单横跨至少25个区块，出现所有ID；断线跨25块后恢复不漏，乱序重复日志只展示一次；时间线包含创建、付款、争议和裁决。纯分段器由`test/EventRanges.ts`测试，证据`T03-index-tests.txt`及BONUS-TIMELINE截图。
  **QA 失败**：模拟中间段RPC失败，checkpoint不越过失败段，页面显示未同步完成；不能把已有列表清空冒充零订单。
  **提交**：`feat: index escrow orders and timelines`。依赖T02。

- [ ] T04 B创建与连续付款（武钰斐）

  **执行**：新增CreateOrderForm和PaymentAction；卖家、金额字符串、到期分钟、描述可填，固定WYFToken；金额parseUnits18并校验正数/精度/uint256，到期以提交时读取的最新链时间加分钟秒数计算。付款使用已有`writeContractAsync`：approve精确金额给当前实例，确认成功才deposit；检查非空hash并捕获receipt。每单互斥，展示授权中/付款中/成功/拒签/失败。第一步后关闭页面允许按链上allowance恢复付款，但正常验收用额度0展示两次真实弹窗。
  **参考**：`useScaffoldWriteContract.ts`及`useTransactor.tsx`已核实语义；04第5.2节及4B-1解释。
  **验收**：付款前后数额、spender、合约实例正确，两个hash分别记录；模拟或授权失败时没有deposit；刷新不重复创建订单；用事件识别实际ID。
  **QA 正常**：30 WYF新订单Created，授权回执成功后第二次签名才出现，付款后Paid且托管余额增30；证据4B-2。
  **QA 失败**：拒绝第一次签名不发deposit；批准后拒绝第二次签名保持Created与真实allowance，能恢复，不把钱包弹窗当成功。
  **提交**：`feat: create and fund escrow orders safely`。依赖T02。

- [ ] T05 B角色、状态与动作（武钰斐）

  **执行**：OrderRow对每单动态显示买家/卖家/仲裁/旁观者，顶部给出当前账户与角色集合，不把某一单角色当全局固定身份。买家Paid可确认和争议，卖家Paid仅争议，arbiter仅Disputed显示两种裁决。断开钱包或错误网络只读并禁写；原合约身份以链上arbiter读取，不硬编码当前钱包为管理员。
  **参考**：原Escrow权限与状态机；04第5.2、5.3节。
  **验收**：地址归一比较；所有成功操作确认回执后刷新状态和余额；前端隐藏按钮不当作合约安全边界。
  **QA 正常**：A/B/C三账户截图同一Paid/Disputed订单，显示的按钮符合4B-3、4B-4；C退款后Refunded，A确认另一单Completed。
  **QA 失败**：本地以非买家直接调用confirm、非仲裁直接resolve应被合约拒绝；只读模拟失败不填上链hash。证据`T05-permissions.txt`。
  **提交**：`feat: enforce escrow role and state actions`。依赖T03、T04。

- [ ] T06 B测试网完整验收与冻结（武钰斐领衔）

  **执行**：每阶段前核对chain/实例/余额；买家需要至少60 WYF，余额不足由owner按记录增发，不能套用实验3旧70余额。从当前orderCount后新建正常单和争议单，实际ID记台账；A创建及付款两单、B争议一单、C退买家、A确认另一单。全部业务通过新页面，成员本人控制钱包；取得resolve真实from及Transfer/OrderResolved日志。
  **参考**：04第5.3节，4B-1—4B-6；T02台账。
  **验收**：7项功能、6组截图、5道解释齐全，截图有角色与实例标签；所有链上结论来自receipt/getOrder/balance；B完成后打基础B标签，合同不再为加分改变。
  **QA 正常**：按初始余额计算两单共托管60、退款30、付款卖家30；余额用差额而非固定70；全部hash能查询。证据`docs/evidence/B/`。
  **QA 失败**：任一环节RPC超时，暂停后按hash或nonce/订单事件核对，不直接重发写入；重新打开页面应找回实际订单。
  **提交**：`docs: record route B acceptance evidence`。依赖T03—T05，需三角色实际操作。

- [ ] T07 A环境、封装与示例（苏佳豪）

  **执行**：`backend/`去除示例明文密钥，properties仅`${WEB3J_PRIVATE_KEY}`；RPC默认POTOS，gasPrice按讲义1000000 wei、gasLimit6721975配置且说明单位，chainId60600；用明确带chainId的TransactionManager。苏创建仅本机持有的新BE钱包并准备测试币，公开地址登记。复制组长原Escrow/WYF源码，固定编译0.8.20/paris，与ABI/bytecode一致，再生成Java wrapper。增加Spring Boot测试依赖JUnit5/Mockito。启动并跑SimpleStorage deploy/set100/get100。
  **参考**：现有Java build.gradle/Web3jConfig/SimpleStorageService/Controller；04第4.2—4.4节。生成包`com.wetech.demo.web3j.contracts.escrow`；字段以实际wrapper为准。
  **验收**：`bash gradlew generateContractWrappers test bootJar`成功；properties截图无密钥；Order及事件解码器存在；SimpleStorage curl与set回执可对应。
  **QA 正常**：4A-1、4A-2、4A-3，记录BE地址、set hash及get100。
  **QA 失败**：缺环境变量须在启动时明确失败，不退回公开测试私钥；错误chainId不发送交易；日志不打印credentials或配置秘密。
  **提交**：`feat: configure backend and contract wrappers`。依赖T01、T02。

- [ ] T08 A六接口与真实回退响应（苏佳豪）

  **执行**：新增`EscrowService.java`、`EscrowController.java`、DTO和异常映射。接口固定为POST`/api/escrow/deploy`、POST`/load?address=&fromBlock=`、GET`/address`、GET`/orders/{id}`、GET`/orders`、POST`/orders/{id}/resolve?sellerWins=`。deploy的arbiter=BE；load验证chain、地址、code及已知方法，切换上下文与写入串行，单请求捕获不可变实例。数额/时间/id用字符串，状态文字。正常resolve回执返回hash/block/status；已上链回退返回422和可查hash、block、status0及实际原因；网络未知结果返回503和已知hash，不声称未发送。参数非法400，未加载409。
  **参考**：04第4.5/4.6节、现有SimpleStorageController与Web3j生成方法；T02 API契约。
  **验收**：六接口均有JUnit/Controller验证。A验收专门对Paid正常单执行一次不合法resolve，以固定gas实际发送并获得status0回执；不能在模拟阶段停止后把它当规定的失败交易。若RPC拒绝广播，记录真实情况并先解决再计该条完成。BE写入串行管理nonce，不自动重发超时写交易。
  **QA 正常**：新部署地址返回arbiter=BE，load相同实例后读到字段正确，Disputed单退款成功；证据`T08-api-tests.txt`。
  **QA 失败**：Paid单resolve的实际失败hash能在浏览器查到；失败不转币、不改状态，响应能区别HTTP成功与链上失败。外部from字符串不能替代Credentials身份。
  **提交**：`feat: implement escrow REST operations and receipts`。依赖T07。

- [ ] T09 A事件列表与时间线接口（苏佳豪）

  **执行**：新增`EscrowEventIndexService`和GET`/api/escrow/orders/{id}/events`。从部署块到当前头按10块分段读取同一实例的全部订单事件，重用索引派生Created列表和每单时间线，去重与排序规则同B。检查JSON-RPC error后才更新checkpoint，缓存按chain/address隔离，重启后可续扫。列表严格返回id/buyer/seller/amount/blockNumber/transactionHash；详情另查当前状态。
  **参考**：04第4.5与6节；实际wrapper的ORDERCREATED_EVENT及解码器；T03跨段验收规则。
  **验收**：事件列表不是循环getOrder冒充；timeline包含全部已发生的适用事件。解释RPC数量：逐单法约1+N次；首次日志法约1+ceil(H/10)次，若还查当前详情另加M次；缓存增量后只扫新块，不能声称事件法永远只请求一次或永远更少。
  **QA 正常**：本地造跨25块、重复与乱序日志，列表无漏单、时间线稳定；一个HTTP events请求返回完整排序。证据`T09-events-tests.txt`与BONUS-TIMELINE-A。
  **QA 失败**：错fromBlock或中段RPC error应可诊断，不能返回成功空数组掩盖错误；缓存不跨A/B/PLUS实例。
  **提交**：`feat: reconstruct escrow orders and event timelines`。依赖T07、T02。

- [ ] T10 A完整业务流与基础总冻结（苏佳豪领衔）

  **执行**：后端部署A_BASE并核对BE；买家在Remix按真实ID创建正常/争议两单各30WYF，授权60后分别deposit；卖家dispute争议单。保存3条GET响应；先对Paid正常单resolve失败，再对争议单resolve(false)退款；买家confirm正常单。完成后再开通扩展的测试网部署。
  **参考**：04第4.6节、4A-5—4A-8；T08失败回执规定。
  **验收**：4A-1—4A-8与6题解释齐全。4A-5保留两次create、两次deposit、dispute；4A-6两单状态清楚；4A-7实际失败及成功；4A-8 From=BE、30代币Escrow到买家和OrderResolved。README八个规定操作均有完整可查hash。
  **QA 正常**：A本金变化与两单总额一致、from/arbiter/recipient不混；`baseline-complete`标签只在T06/T10均通过后建立。证据`docs/evidence/A/`。
  **QA 失败**：停服务重启后load已部署A实例和真实起始块能重建订单；不会偷偷部署另一实例导致原台账失效。失败交易的gas由BE承担，未执行业务不等于没有消耗gas。
  **提交**：`docs: capture complete route A acceptance`。依赖T08、T09。

- [ ] T11 PLUS发货状态及测试（武钰斐）

  **执行**：新增`contracts/EscrowPlus.sol`，参考原实现但独立部署，复用IERC20接口。追加Shipped5；`markShipped(id)`只允许卖家、Paid、`block.timestamp <= deadline`，发OrderShipped。confirm允许买家在Paid/Shipped确认；dispute允许双方在Paid/Shipped争议；refund仅买家Paid且严格超过deadline，Shipped须通过争议裁决；状态先变再外部转账。BASE文件不变。
  **参考**：原Escrow.sol状态机；04/07发货加分；新测试`test/EscrowPlus.ts`。
  **验收**：原8项回归全过；新增发货正反例、超时边界、Shipped确认/争议均有断言；对PLUS不套用BASE的五状态数组导致5越界。生成独立tag`EscrowPlusWYF202492451119`。
  **QA 正常**：Paid->Shipped->Completed支付卖家30；另一个未发货单过期refund退买家；本地时间工具只用于本地测试。证据`T11-shipping-tests.txt`。
  **QA 失败**：非卖家、重复发货、过期后发货失败；Shipped过期普通refund仍失败、资金不动；不要把模拟失败标成已上链。
  **提交**：`feat: add shipped escrow state and regression tests`。依赖T06、T10。

- [ ] T12 PLUS两人一致仲裁及测试（武钰斐）

  **执行**：PLUS构造参数两名非零且不同的仲裁地址；`resolve(id,sellerWins)`仅这两名之一、Disputed有效。第一票存decision并发ResolutionVote，未转账；不同意见则保持Disputed；执行前允许签署者更新本人意见，达到两人均投且相同才改终态、转账一次、发OrderResolved。票据按订单隔离，展示已投成员及方向；不接受前端传sender冒充身份。
  **参考**：07多签要求“两人都调用resolve且意见一致”；T11 PLUS存储、现有resolve资金路径。
  **验收**：苏、武分别持有PLUS专用MS1/MS2，均与A后端BE不同，真实签名；不用单个服务器Credentials伪装两人。新增测试：单票不转币、重复同一人不算第二票、分歧不结算、更新达成一致、不同订单票隔离、已结算不能再执行、非仲裁失败。还要验证false退款和true支付两条分支。
  **QA 正常**：第一人false后Disputed且托管30；第二个不同地址false后Refunded且买家+30，仅一次最终Transfer。证据`T12-votes-tests.txt`及两笔真实hash。
  **QA 失败**：先false后true保持Disputed与余额不变；同一地址调用两次不出款；随后更新一票一致才结算，不靠永久分歧锁死作为成功演示。
  **提交**：`feat: require two matching arbitration votes`。依赖T11。

- [ ] T13 PLUS页面与真实加分演示（武钰斐）

  **执行**：新增`app/escrow-plus/page.tsx`及独立PLUS适配器，复用列表/表单小组件但不修改BASE ABI。页面显示实例、Shipped、卖家发货按钮、两名仲裁地址与当前票，第一票明确显示待另一人确认，分歧显示未结算；苏连接MS1、武连接MS2本人签名。PLUS全部事件也纳入时间线。部署前核对两个仲裁地址、字节码和测试结果。
  **参考**：T03—T05页面交互、T11/T12新ABI、07三项3分加分。
  **验收**：测试网三组互不混淆的订单：发货->确认；发货->争议->两人一致裁决；未发货过期退款。发货后超期退款拒绝的证据必须明确业务原因，不能用RPC失败充数。短期订单留足操作余量；实际到期以链时间为准。
  **QA 正常**：BASE/PLUS切换不会串状态与地址；第一票前后资金不变，第二票后转账；时间线按顺序含Shipped、两票及最终Resolved。证据BONUS-SHIPPED、BONUS-MULTISIG、BONUS-TIMELINE-B。
  **QA 失败**：卖家看不到仲裁按钮，非签署者绕过UI仍被链拒绝；错误链禁写；拒签一票不把它算作已投。每个失败标注模拟/上链性质。
  **提交**：`feat: demonstrate shipping and shared arbitration UI`。依赖T03、T11、T12。

- [ ] T14 受控重入金库与本地复现（苏佳豪）

  **执行**：新增VulnerableVault、FixedVault、Attacker及`test/Reentrancy.ts`。漏洞版本先call再清余额；修复版本先清零再call。Attacker构造绑定本组金库，attack先deposit再withdraw，receive仅在金库足额且回调次数小于固定上限时再withdraw。固定最多3次提取，不写无界循环。测试明确攻击者本金、受害者本金、攻击合约余额和金库余额；生成新部署tag，不覆盖业务Escrow。
  **参考**：04第6.1节。正式步骤受害者0.002POT、攻击0.001POT，合计0.003POT；讲义注释中0.0001为另一示例金额，不能混写同一轮数据。
  **验收**：漏洞版完成后vault=0、attacker=0.003POT且有多次回调证据；修复版同一策略回退。由于attack整体回滚，修复金库应保留受害者原0.002POT，攻击者本次0.001存入也回滚，不误写固定金库应有0.003。普通用户正常存取仍成功。
  **QA 正常**：`yarn hardhat:test`含3次回调、资金守恒、修复拒绝与正常提款断言；证据`T14-reentrancy-tests.txt`。
  **QA 失败**：攻击者地址/金库地址错误、零额attack、无余额withdraw均明确失败；拒绝攻击不得误判正常取款全坏；不操作第三方未知合约。
  **提交**：`test: reproduce and fix controlled vault reentrancy`。依赖T01。

- [ ] T15 重入测试网两轮证据（苏佳豪领衔）

  **执行**：确认本组两钱包测试POT足额（建议各准备约0.01POT覆盖两轮本金及部署gas，具体按当时余额和费用估算），分别部署漏洞金库/攻击合约、修复金库/新攻击合约。武账户存受害者0.002，苏控制攻击账户用0.001执行；两轮分开记录contract、hash、余额及gas。只针对本组新建练习合约；金库实验资金不与托管业务混用。
  **参考**：04第6.1节4C-1—4C-3；POTOS Blockscout不索引内部交易的课程说明。
  **验收**：4C-1展示存款与漏洞攻击后余额；4C-2如Internal Transactions为空，原样保留并明确该浏览器限制，以真实余额差及T14回调证据补充，不能绘制假调用列表；4C-3有修复后真实失败交易和资金保持证据。
  **QA 正常**：成功attack前后vault0.003->0，attacker0->0.003；买方实际本金与转入明细相符。证据`docs/evidence/C/`及台账。
  **QA 失败**：修复后同一策略status0、vault仍0.002、攻击合约0；若仅模拟失败尚无hash，不记为正式4C-3已上链证据，补做真实受控发送并核验回执。失败gas属于攻击交易发起者。
  **提交**：`docs: capture vault attack and fix evidence`。依赖T14、基础冻结。

- [ ] T16 最终集成、文档与答辩（武整合、苏复核、杨做实际记录）

  **执行**：README提供环境版本、前端/后端启动、环境变量名称但无值、真实地址与部署块、B/A/PLUS/C入口、API示例、八行及扩展完整交易表；写报告全部4A解释6题、4B解释5题及4C原理，五加分独立章节。每道解释关联本组截图编号、实际数值、操作者与角色。报告末尾单列“AI使用说明”，依据`docs/ai-usage-log.md`写实际工具、用途、真实错误及人工发现/修正过程；缺失按07扣2分。杨记录本人卖家操作时间、截图编号、实际审阅条目；不分配虚构代码贡献。提交前按PR/提交/钱包回执回填分工表。
  **参考**：04第7节、07全部评分项和AI政策；T02、T06、T10、T13、T15证据。
  **验收**：苏在干净clone照README运行前端，武照README运行后端，自动检查命令全通过；报告与README完整hash/真实ID/from/状态/金额一致；秘密扫描含Git历史通过；助教可访问仓库；报告首页与邮件正文均有URL。所有截图原始保留，未执行检查明确标注，不凭HTTP200/RPC失败推断链上业务结果。
  **QA 正常**：逐项打开4A-1—8、4B-1—6、4C-1—3和三项3分截图，核对可读性；按台账查回执；三人各能解释本人实际任务。证据`docs/evidence/final-checklist.md`。
  **QA 失败**：第二人从干净环境缺配置、旧地址、错误网络、未知状态5、缺少某票/某行hash时必须标红并修正；不以有文件名或截图标题代替实际内容。
  **提交**：`docs: finalize reproducible capstone submission`。依赖T06、T10、T13、T15。

## 解释题写作检查点

- 4A-1：公开示例密钥不具私密性；服务器仲裁权的责任；只写地址不写密钥。
- 4A-2：Java结构体字段与实际生成Order对应；事件签名、indexed参数与解码依据。
- 4A-3：RPC数量按区块跨度、订单数与缓存计算，不把日志查询一概说成一次请求。
- 4A-4：以本组错误状态仲裁的实际异常和receipt说明是否上链、gas和付款人；区分模拟拦截。讨论恶意请求造成费用与nonce压力。
- 4A-5：From=BE，token转出者=Escrow、接收者=买家；标注本组实际Web3j签名配置与生成wrapper调用路径。
- 4A-6：至少两层：接口认证/操作授权 + 限流/审计/额度控制；泄露仲裁密钥可裁决符合条件的争议单，不代表存在任意提现或绕过订单状态的接口。
- 4B-1：两个独立交易及确认顺序；关闭页面后approve可能已生效、订单仍Created；恢复时读allowance，不把授权等同付款。
- 4B-2：前端权限为交互提示，链上检查才有约束；修改页面不改变msg.sender和角色。
- 4B-3：B由仲裁人钱包签名；A由服务BE签名。两者都看实际from，不能把发HTTP请求的人写成链上发送者。
- 4B-4：页面外创建也会产生链上事件，索引正确且追赶完成后应可见；缓存不是独立事实来源。
- 4B-5：公开前端无需私钥；看到源码不等于取得签名权，但链上授权、合约缺陷或恶意钱包签名仍须分别分析。
- 4C：解释回调时旧余额未清导致重复提款、CEI修复与重入锁等防御；用本组0.002/0.001/0.003数据，修复回滚的本金与gas分别说明。

## 最终验收

- F1 逐项核对04/07及上表，五项加分各有独立证据，不把21名义分写成可加21分。
- F2 测试、构建、错误路径和密钥扫描通过；前端无私钥，后端真实from等于BE，多签为两个不同实际签名人。
- F3 真实钱包完成A/B及PLUS；检查拒签/超时/断线恢复，不能用RPC连接失败证明业务检查。
- F4 README由苏在干净目录照做一遍，武核对Java；三名成员各讲清本人实际负责部分。截图/数字/台账/地址一致。
- F5 用户已同意公开；提交前用未登录浏览器确认仓库与README、代码、证据均可访问。苏可从本人账号fork并向主仓库提PR；不把公开可读误写为任何人可直接push。
- F6 按模板提交`班级_28_武钰斐_202492451119_大作业报告.docx`，邮件主题与文件名对应，仓库URL同时写首页和邮件正文。
- F7 独立“AI使用说明”存在且内容真实；11道A/B解释题逐题具备本组截图具体数值、材料所属成员与角色。班级、模板、截止时刻已确认；11月7日晚内部交付，11月8日准时提交并保留提交记录。

## 提交与执行边界

本轮只完成规划及用户明确授权的仓库准备。未实现产品、未部署新合约、未邀请未知用户名、未验证他人是否已完成任务。正式开工从T01清理导入和T02注册表开始；后续实现时适用编程、调试与实施后复核技能。计划中的新路径均为待创建文件，不冒称已存在。
