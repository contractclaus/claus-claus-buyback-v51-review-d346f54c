# CLAUS v51 buyback source review

This repository contains the exact two proposed contracts and verified baseline sources for the existing CLAUS pool on Robinhood chain 4663. The proposed contracts are not activated yet.

## Exact reproducible build

Use solc 0.8.26 with each complete standard JSON input in build/hook.standard-input.json and build/vault.standard-input.json. Each input deliberately contains both source units and the exact remappings, output selection, metadata and optimizer configuration. Generic forge defaults are not the original build. The complete artifacts and their canonical artifact hashes, full runtime hashes and metadata-stripped hashes are in build/. The inputs have been recompiled locally and the full creation and runtime bytes matched the original declared artifacts exactly.

## Corrected deployment and authority

The new vault constructor owner is the existing ClausAdministrator 0x979D5810D32292358639f25294472f01c95bDc46, preserving founder recovery and global operator revocation. Before delegation is used, the founder must register the deployed new vault with setTarget(newVault,true). The operator cannot self-register it. The keeper is the existing full 20-byte address 0xAc796F7ac40c0CE9cdc0Dbe61d8bc7C98dC5CBc5. Pool and maxBatch=0.5 ETH remain unchanged. review-context.json is the exact corrected context. The earlier review context's malformed keeper and direct operator ownership are superseded.

## Activation is a separate, receipt-verified step

The old vault is correctly still enabled and selected before the upgrade. Review the proposed source and planned transition; do not mistake this pre-activation state for a claim that the new contracts are already live. Activation requires the exact deployed runtime hashes, new owner and target registration to be verified, the worker paused and drained, and one administrator batch disabling the old vault, upgrading the existing hook, selecting the new vault and recovering unspent old-vault ETH into it. No LP position withdrawal is included. The original SQLite journal and cumulative history must survive. Actual receipts are required after activation.

Ordinary trades retain a 2% fee split equally between buyback/burn and treasury. The sole configured vault's immediate authenticated buyback swap is exempt from that fee, so buyback funds are fully spent on the purchase rather than taxed into another self-payment. The entire transaction reverts on partial fill. This is the intended economic change, not a claim that protocol buybacks still pay the trading fee.

The source snapshot and deployed baseline proofs are retained. Current public notice: https://x.com/i/status/2119153958392398291. Active upgrade cannot occur before 2026-11-07T21:00:00Z and before an independent review passes.
