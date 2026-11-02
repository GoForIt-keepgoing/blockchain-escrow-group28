# Backend starter

Imported from the existing course example in Ubuntu:
`/home/yunjy/blockchain-course/spring-boot-web3j`.
Source repository commit: `a36f03e5c26a9df77dd6acc17c4b1a4eef6616af` (local working files were used).

This is the SimpleStorage starter, not the completed Escrow backend.
Java 21, Spring Boot 3.2.3, Web3j 4.14.0 and Gradle Wrapper 8.13 are retained.
Old Git history, build output, caches and logs were excluded.
The embedded private key and its code fallback were removed before import.
Gas price is 21000 wei; gas limit is 6721975.

## Windows PowerShell

```powershell
cd backend
.\gradlew.bat --version
# Compile and package the existing generated SimpleStorage wrapper.
.\gradlew.bat compileJava test bootJar -x generateContractWrappers -x generateTestContractWrappers -x compileSolidity -x compileTestSolidity
```

The imported SimpleStorage.java is generated code from the old project.
The check above does not regenerate or validate Solidity bytecode.
Pin Solidity 0.8.20 and EVM paris and regenerate wrappers before deployment
as part of the next contract-configuration step.
No automated Java tests are included in this starter yet.

## Existing local cache

The first distribution download timed out. This computer's existing Ubuntu
Gradle 8.13 distribution and Maven dependency caches were copied outside
the repository to `D:/课程学习/区块链技术与应用/tmp/backend-gradle`.
To reuse that cache from PowerShell, set `GRADLE_USER_HOME` to that directory
and append `--offline` to the compilation command above. No global Gradle
installation is needed.

## Runtime configuration

`src/main/resources/application.properties` reads `WEB3J_PRIVATE_KEY`
from the local environment, with no default key. Missing configuration
must prevent startup. Set it locally; never put it into source files,
screenshots, commits or chat. No key is needed for compilation.
After completing the remaining compiler/chain configuration and setting the account locally, use `.\gradlew.bat bootRun`.
This service can submit transactions when its write endpoints are called.
No deployment or chain transaction was performed during import.

## Remaining work

Confirm the group contracts and interface agreement; configure explicit
chain ID and compiler settings; then implement Escrow wrappers, endpoints
and tests following ../docs/PROJECT_PLAN.md.

## AI assistance

Codex imported the starter, removed hardcoded key settings, adjusted the
gas configuration, and checked the local build. Results are recorded in
../docs/evidence/backend-import-check.md.
