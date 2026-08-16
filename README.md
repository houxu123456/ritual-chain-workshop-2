# Ritual Predict — Bootcamp Level 2 Assignment

**Completed by:** [hx / hou_289215488]  
**Date:** August 16, 2026  
**Ritual Academy:** Bootcamp Level 2 (Self-Resolving Prediction Market)

## What I did
- Forked the official workshop repository
- Reviewed the full architecture: Scheduler → HTTP precompile → jq precompile → settlement
- Studied the design decisions around block-based deadlines, retry mechanism (3 attempts), and pull-based payouts
- Ran through the local test suite with mocks (hardhat test)
- Prepared the project for mainnet deployment once the network is live

## Key learnings
- Deadlines use block numbers instead of timestamps for reliability
- Failed oracle reads are treated as Invalid (refund) rather than NO
- Execution fees are prepaid via RitualWallet
- No hardcoded executors — dynamic selection via TEEServiceRegistry

## Repository status
Ready for mainnet. Testnet was already closed at the time of completion.
