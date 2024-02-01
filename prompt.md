The Polkadot and Kusama relay chain currently contains functionality that may be considered
extraneous, such as staking, governance and name registry. To reduce the processing load on the
relay chain, these extra functionality will individually be spun out into its own system parachain.
In this assignment, we shall focus on the attempt to decentralize staking by creating a new system
parachain whose sole purpose is to process staking. We shall call this parachain Stake Hub.

1. Discuss whether the staked relay chain tokens should be used as a derivative, or be teleported
as-is to Stake Hub. Provide justifications for your answer.

a. Which location should be holding the funds used for staking?

2. Given that the first step of the user is to call the `bond` dispatchable with its function
signature shown below:

```rust
#[pallet::call_index(0)]
pub fn bond(
    origin: OriginFor<T>,
    #[pallet::compact] value: BalanceOf<T>,
    payee: xcm::Location,
) -> DispatchResult;
```

and assuming that the staking pallet is at index 7 of the Stake Hub runtime, create a dispatchable
function `bond_remote` that allows the user to hold up the funds in the way described in (1a) and
instructs Stake Hub to start staking the funds provided to the dispatchable.

a. Attempt to make the XCM program resilient, e.g. failing gracefully when there are insufficient
funds, or the pallet/call index in the receiving chain is different than expected.

b. Design an XCM instruction that would facilitate the cross-chain bonding process.

3. Users will periodically receive rewards for their stake every era. Discuss where the rewards
shall be paid to, and how the user can claim the rewards.
