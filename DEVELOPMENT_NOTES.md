# Development Notes

## Market Lifecycle

I started by mapping the market lifecycle because the resolution process was
not immediately obvious to me.

The basic flow is:

1. Create a market.
2. Store the resolution parameters.
3. Accept YES and NO bets.
4. Wait until the resolution block.
5. Let the Scheduler trigger the resolution.
6. Select an executor capable of making the required HTTP request.
7. Retrieve the external response.
8. Extract the required value from the response.
9. Compare the value with the configured target.
10. Resolve the market.
11. Allow users to claim their rewards.

## Market Parameters

A market needs enough information to resolve itself later.

The important parameters include:

- target value
- comparator
- oracle URL
- JSON path
- resolution block

These parameters should describe the question being asked by the market.

## Why the JSON Path Matters

The HTTP response may contain much more information than the market needs.

The JSON path tells the resolution process which value should be extracted.

For example, an API response could contain price, volume, timestamp and other
fields.

The market only needs the configured field.

## Scheduler

The Scheduler is responsible for triggering future execution.

This means that the market does not depend on a separate server running a cron
job.

The contract can prepare future resolution attempts when the market is
created.

## Retry Logic

A single external request is not always reliable.

A request can fail because of:

- temporary network problems
- an unavailable endpoint
- invalid response data
- executor failure

For this reason, multiple scheduled attempts are useful.

## Resolution

The final result should be based on the configured comparison rule.

A successful external response produces a value.

The contract then compares that value against the target.

The result becomes either YES or NO.

## Invalid Resolution

A failed external request should not automatically become a NO result.

This distinction is important because an unavailable oracle does not mean the
prediction was false.

An invalid market should instead follow the refund rules defined by the
contract.

## Claims

The payout mechanism uses a pull model.

Users claim their own rewards instead of the contract sending rewards to every
participant in one transaction.

This reduces the amount of work required during settlement.

## Things I Want to Test

The main cases I want to verify are:

- market creation
- YES betting
- NO betting
- deadline enforcement
- successful resolution
- failed resolution
- invalid market
- refund
- reward claim
- duplicate claim

## Personal Notes

The most useful part of the workshop so far has been understanding how the
external data flow connects back to deterministic contract logic.

The market itself does not need to know how HTTP works.

It only needs the result produced by the Ritual execution environment.
