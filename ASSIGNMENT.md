# Bootcamp Level 2 Assignment Notes

## Project Summary
Built and reviewed a self-resolving binary prediction market on Ritual Chain.

## Core Flow I understood
1. createMarket() — sets question, oracle, target, and schedules resolution
2. Users bet YES/NO with native RITUAL
3. Scheduler wakes the contract at resolveBlock
4. Contract calls HTTP precompile → jq extracts value → compares with target
5. Market resolves or becomes Invalid after 3 failed attempts
6. Winners claim proportional share

## Why this design is interesting
- Fully on-chain resolution, no backend or manual resolve button
- Uses Ritual’s native Scheduler and precompiles
- Handles failures gracefully with retries and refunds

## Next steps
Waiting for Ritual mainnet to deploy and test live.
