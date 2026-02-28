# Bidder Leaderboard Playbook

Use this file as handoff context for any future AI agent.

## Goal
When seller confirms $1,000 deposit, add bidder to leaderboard and optionally start 4-hour winner countdown.

## Source File
- Update logic lives in [index.html](index.html).

## Current Behavior
- Bid form emails submissions to `tomgouldmaui@gmail.com`.
- Leaderboard data is stored in browser local storage.
- Helper function exists in page script:
  - `addApprovedBidder(name, amount)`
- If `amount >= current ticker price`, ticker pauses and 4-hour countdown starts.

## What to tell the next AI agent
Use this exact prompt:

"In [index.html](index.html), add bidder NAME with amount AMOUNT using the existing `addApprovedBidder(name, amount)` workflow, and make sure leaderboard shows them correctly. If this bid should be the leader, start the 4-hour countdown. Then commit and push."

## Manual Browser Command (quick)
In browser devtools console on the site:

`addApprovedBidder('Bidder Name', 8800)`

## Reset / Remove Leader
If seller asks to remove active leader:
- Clear active auction state in local storage key `oc_auction_state_v1` (set inactive)
- Change any `Leading`/`Winner` bidder status back to `Approved`
- Remove bidder entry if requested

## Notes for future agent
- Do not add automatic admin approval UI unless user asks.
- Keep only 4-hour winner countdown (no 12-hour lock window).
