# Resolution Test Cases

## Market Creation

### Case 1

Create a market with valid parameters.

Expected result:

The market should be created successfully.

### Case 2

Create a market with an invalid resolution block.

Expected result:

The transaction should fail.

## Betting

### Case 3

Place a YES bet before the deadline.

Expected result:

The YES pool increases.

### Case 4

Place a NO bet before the deadline.

Expected result:

The NO pool increases.

### Case 5

Try betting after the deadline.

Expected result:

The transaction should fail.

## Resolution

### Case 6

Resolve using a valid oracle response.

Expected result:

The market becomes resolved.

### Case 7

Resolve with an HTTP failure.

Expected result:

The failure should not be interpreted as a valid NO result.

### Case 8

Resolve with malformed JSON.

Expected result:

The market should not settle using invalid data.

### Case 9

Use a JSON path that does not exist.

Expected result:

The resolution attempt should fail safely.

## Claims

### Case 10

A winning user claims rewards.

Expected result:

The user receives the calculated reward.

### Case 11

The same user tries to claim again.

Expected result:

The second claim should fail.

## Invalid Markets

### Case 12

The resolution process cannot determine a valid result.

Expected result:

The market becomes invalid according to the contract rules.

### Case 13

A user attempts to claim from an invalid market.

Expected result:

The user receives the appropriate refund.

## Access Control

### Case 14

An unauthorized address attempts a privileged operation.

Expected result:

The transaction should revert.

## Repeated Resolution

### Case 15

A resolved market receives another resolution callback.

Expected result:

The market state should not be changed again.

## Scheduler

### Case 16

The first scheduled attempt fails.

Expected result:

A later attempt remains available.

### Case 17

An attempt succeeds.

Expected result:

Further unnecessary attempts should be cancelled.

## Regression

Every new contract change should be checked against the existing market
behavior.

A new feature should not change:

- betting rules
- deadline rules
- payout rules
- invalid-market behavior
