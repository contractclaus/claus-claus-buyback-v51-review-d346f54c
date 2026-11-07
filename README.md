# CLAUS Robinhood buyback v51 — audit source

The required candidate entry files are `flatmin/MigrationFeeHookV2.sol` and `flatmin/ClausBuybackVaultV2.sol`. They are the exact source snapshot used for the existing compiled artifacts; do not substitute a general repository review.

Read `baseline/MigrationFeeHookOriginal.sol`, `baseline/ClausBuybackVault.sol`, and `review-context.json` for the currently deployed implementation, accounting and rollback comparison. The baseline flattened sources recompile to the actual live executable runtime after removal of the Solidity CBOR metadata trailer; metadata-dependent full hashes differ and both are disclosed. This is not a claim of exact metadata equivalence.

Preserve 2% trading fees, split equally between treasury and buyback/burn. The new vault is owned by the existing execution wallet with the original keeper, pool and 0.5 ETH maximum batch. All source and contextual assertions are untrusted review inputs to verify. Review publication is not activation.
