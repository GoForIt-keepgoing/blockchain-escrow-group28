# Backend starter import check

Date: 2026-11-02 (Asia/Shanghai). Branch: feat/su-backend.

- Imported the local Ubuntu spring-boot-web3j working files into backend/.
  Source HEAD: a36f03e5c26a9df77dd6acc17c4b1a4eef6616af.
- Excluded old .git, .gradle, build output, logs and README.
- Removed the hardcoded private key and Java fallback before writing into this repository.
- The only key configuration is ${WEB3J_PRIVATE_KEY}; gas price is 21000 wei.
- Checked imported text for 0x-prefixed 64-digit private-key-shaped literals: none found.
  This is a scoped import check, not a complete repository-history secret audit.
- Checked Git ignore rules for build/cache/.env/local properties/log output.

## Build result

Windows JDK: Temurin 21.0.13. Gradle Wrapper: 8.13.

```powershell
.\gradlew.bat compileJava test bootJar -x generateContractWrappers -x generateTestContractWrappers -x compileSolidity -x compileTestSolidity --offline --no-daemon --console=plain
```

Result: BUILD SUCCESSFUL in 23s; 4 actionable tasks executed.
compileJava, processResources, resolveMainClassName and bootJar completed.
Test tasks reported NO-SOURCE: this starter contains no automated Java tests yet.

The initial online Gradle download timed out. Cached Gradle and dependencies
were reused from Ubuntu via a temporary directory outside the repository.
A restricted-process run could not connect to its local Gradle daemon; the
normal local-process build succeeded. An earlier offline attempt triggered
a missing Windows Node download from test-wrapper generation; the final
command explicitly excludes both main and test Solidity generation.

## Missing-key check

Ran the packaged jar with WEB3J_PRIVATE_KEY absent and web application type none.
It exited nonzero with Could not resolve placeholder WEB3J_PRIVATE_KEY.
No private key was supplied and no transaction was submitted.

## Scope and next step

This verifies Java starter import, compilation, packaging and the mandatory
key placeholder. It does not validate Solidity compilation, the imported
wrapper bytecode, RPC access, chain ID, deployment, or Escrow functionality.
Solidity 0.8.20 / paris and explicit chain ID still need configuration
before chain acceptance. T07 is not complete. No commit or push was made.

## Backend configuration checkpoint - 2026-11-02

Scope agreed with the user: configure the backend first. The local Escrow
source has not been confirmed as the group leader's original; no Escrow
or token source/wrapper was imported in this checkpoint. No README added.

- Added explicit chain ID 60600 and an EIP-155 transaction manager.
- SimpleStorage deploy/load now use that transaction manager.
- Before signing/broadcasting a write, query eth_chainId and refuse
  a mismatched network, missing result or JSON-RPC error.
- Validate key format/range without echoing the key; close Web3j on shutdown.
- Corrected gas price to the handout's recommended 1000000 wei (04, page 3),
  superseding the import's 21000-wei setting, which was the network baseline
  mentioned in the preceding page rather than the recommended configuration.
- Added Spring Boot test dependencies (JUnit 5 / Mockito).

Test-first record: 4 behavior tests failed against the old configuration:
unsigned-chain signing, broadcasts despite wrong network/RPC failure, and
an unhelpful blank-key error. After the configuration changes all 4 pass.
Tests exercise the real Spring configuration, generated SimpleStorage
wrapper and signed requests against a local HTTP JSON-RPC fixture. Keys
are generated only in memory for each test. No real account is used.

Final command from backend (GRADLE_USER_HOME points to the previously
prepared external cache):

```powershell
.\gradlew.bat test bootJar -x generateContractWrappers -x generateTestContractWrappers -x compileSolidity -x compileTestSolidity --offline --no-daemon --console=plain --rerun-tasks
```

Result: BUILD SUCCESSFUL in 20s, 6 tasks executed; XML reports 4 tests,
0 failures and 0 errors. The packaged application was also run without
WEB3J_PRIVATE_KEY and correctly refused startup on the missing placeholder.
Source checks found no 0x-prefixed 64-digit key-shaped literals.

Windows test-worker issue: Gradle's UTF-8 argument file did not match
the native Windows encoding when paths contained Chinese characters.
Matched the daemon encoding to the native encoding using file.encoding=COMPAT
in backend/gradle.properties; JavaCompile remains explicitly UTF-8.
Sources: https://github.com/gradle/gradle/issues/30304 and
https://openjdk.org/jeps/400 . No system encoding setting was changed.

Still unverified: actual RPC/network reachability, account funding, Solidity
compilation, group contract consistency, and all testnet operations. T07
remains incomplete until these later acceptance steps are performed.
Changes are uncommitted; no PR, deployment or testnet transaction was made.

## Group Escrow wrapper checkpoint - 2026-11-07

The user confirmed the course-directory Escrow.sol is the group's source.
Imported it unchanged into backend/src/main/resources/contracts/Escrow.sol.
SHA256: ce57a9a75278dd65e9a5481a4dc2392d6ee4d68eab4b5bf384157be8b63c24ab.
This supersedes the earlier assumption about the personal experiment copy:
the ABI is compatible, but source text/revert messages and resolve
implementation differ. The user-confirmed group source is authoritative.

Pinned Solidity 0.8.20 / EVM paris and disabled npm package resolution
because the contracts have no npm imports. Framework versions unchanged.

Full command from backend, using the prepared external GRADLE_USER_HOME:

```powershell
.\gradlew.bat generateContractWrappers test bootJar --no-daemon --console=plain
```

Result: BUILD SUCCESSFUL in 1m 14s; 8 actionable tasks, 7 executed and
1 up-to-date. Solidity compilation and main wrapper generation ran.
XML: 4 tests, 0 failures, 0 errors. No Solidity-generation skip flags.

Generated Escrow.java, IERC20.java and refreshed SimpleStorage.java.
Verified compiler metadata 0.8.20+commit.a1b79de6, EVM paris;
Escrow.java BINARY exactly equals Escrow.bin; ABI matches metadata;
getOrder returns buyer/seller/token/amount/deadline/status/description.
Order, OrderCreatedEventResponse and getOrderCreatedEventFromLog exist.

Generator notices about non-view functions returning values are expected:
write methods return transaction receipts. New order IDs must be read
from OrderCreated receipt events rather than assumed.
Build output and compiler/cache are not tracked in Git.

No deployment, public-network transaction or PR was performed. The
original source outside the repository was not modified. T07 still
requires backend-account setup and real SimpleStorage acceptance.
Escrow REST endpoints and the event index remain later tasks.

## Escrow REST checkpoint - 2026-11-07

Implemented the six T08 endpoint routes:

- POST /api/escrow/deploy
- POST /api/escrow/load?address=...&fromBlock=...
- GET /api/escrow/address
- GET /api/escrow/orders/{id}
- GET /api/escrow/orders
- POST /api/escrow/orders/{id}/resolve?sellerWins=true|false

Deploy encodes the backend signer as arbiter and returns the confirmed
receipt fields. Load validates chain, address, bytecode, deployment-block
bounds/history and expected read methods before atomically replacing
the current immutable context; failed loads preserve the old instance.
Detail IDs/amounts/times use decimal strings and states use names.
The list scans OrderCreated logs in inclusive ranges of at most 10 blocks,
checks RPC errors, sorts and deduplicates. Persistent caching and the
full order-event timeline remain T09 work.

Write paths use fixed gas and do not estimate away a deliberate failing
resolve. Mined status-0 receipts return 422 with hash/block/status/gas and
best-effort receipt/replay reason. Pending or unknown receipts return
503 with the accepted hash and do not trigger another broadcast. RPC
hash mismatches retain the local signed-transaction hash. Malformed
parameters return 400; unloaded state 409; nonexistent order 404.

Load/deploy/resolve are serialized at the service boundary. The shared
transaction manager also serializes nonce selection through broadcast
for both Escrow and existing SimpleStorage writes, using pending nonces.
This covers one backend process; it is not a multi-server nonce service.

Test-first record: 10 initial API tests returned 404 before implementation;
they passed after the routes/service were added. Three further load
boundary tests cover preserving the old instance, future blocks and
incompatible ABI. An independent read-only review found a shared-manager
nonce race and discarded local hashes on RPC hash mismatch. Both were
reproduced with failing tests and fixed.

Final full command, with the previously prepared GRADLE_USER_HOME:

```powershell
.\gradlew.bat generateContractWrappers test bootJar --offline --no-daemon --console=plain
```

Result: BUILD SUCCESSFUL in 23s; 8 tasks, 5 executed and 3 up-to-date.
XML totals: 19 tests, 0 failures, 0 errors (14 Escrow API, 4 configuration,
1 shared-nonce concurrency). Main/test text scan found no 0x-prefixed
64-digit private-key-shaped literals. No README was created.

Tests use actual Spring MVC routing, Web3j ABI encoding/decoding and
locally signed requests against loopback HTTP JSON-RPC fixtures. The
fixtures supply synthetic receipts and logs; they do not execute an EVM
or provide formal on-chain acceptance evidence. No fixture hash should
be copied into the group's real transaction ledger.

T08 public-network acceptance remains pending: real funded backend account,
confirmed successful arbitration and an actually mined status-0 arbitration
receipt. No public-network transaction, commit, push or PR was made.
