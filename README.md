## Minimal Example for foundry-zksync Issue #1081

This repository was created to reproduce [foundry-zksync issue #1081](https://github.com/matter-labs/foundry-zksync/issues/1081).

## Issue Description

**Problem:** Running `forge test --zksync` crashes with an "unwrap panic" in the zkSync cheatcode runner, specifically failing to find a contract.

**Expected Behavior:** The test should revert or fail with an assertion, not crash the entire process.

**Actual Behavior:** The application panics with the error message: "failed finding contract for 0x6080604052..."

**Error Location:** `crates/strategy/zksync/src/cheatcode/runner/mod.rs:573`

**Environment from Original Report:**
- Forge Version: 1.0.0-foundry-zksync-v0.0.20
- OS: Ubuntu 24.04.1 LTS (WSL2)
- zkSolc: 1.5.15

## Reproduction Steps

1. Enable zkSync support in `foundry.toml`:
```toml
[profile.default.zksync]
enabled = true
codegen = "evmla"
```

2. Run `forge test --zksync`

## Current Status

**⚠️ ISSUE NOT REPRODUCED**

This repository has the correct zkSync configuration but the tests **pass successfully** instead of crashing with the reported panic. This suggests either:

- The issue has been fixed in recent versions
- Specific conditions are needed to trigger the panic that aren't present in this minimal setup
- Additional configuration or contract patterns are required

## Test Results

```bash
$ forge test --zksync
No files changed, compilation skipped
No files changed, compilation skipped

Ran 2 tests for test/Counter.t.sol:CounterTest
[PASS] testFuzz_SetNumber(uint256) (runs: 256, μ: 993879674, ~: 993873225)
[PASS] test_Increment() (gas: 993869761)
Suite result: ok. 2 passed; 0 failed; 0 skipped; finished in 870.09ms (600.55ms CPU time)

Ran 1 test suite in 875.08ms (870.09ms CPU time): 2 tests passed, 0 failed, 0 skipped (2 total tests)
```

## Repository Structure

- `src/Counter.sol` - Simple counter contract
- `test/Counter.t.sol` - Basic tests for the counter
- `foundry.toml` - Configuration with zkSync enabled

## Usage

### Build
```shell
forge build
```

### Test with zkSync
```shell
forge test --zksync
```

### Test without zkSync
```shell
forge test
```

---

**Note:** If you can reproduce the issue with different conditions, please let us know what's missing from this setup!
