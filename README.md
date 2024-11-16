# Trustless Bridge

Trustless Bridge bridges ETH from Optimism to Scroll leveraging L1SLOAD precompile.

This is a monorepo for both smart-contracts and frontend.

## Demo video

https://youtu.be/07ohcE1I7_Y

## Workflow

<img title="workflow" alt="workflow" src="./images/scheme.png">

1. User wants to transfer ETH from OP to Scroll, clicks “bridge” button in UI, which triggers a transaction in OP network. ETH moves from user’s address to the bridge contract, and corresponding  note of deposit appears in the bridge contract storage.
2. UI waits for OP network to trigger change of its state root in L1. Once it happens, a button to claim appears on UI.
3. User clicks on the button “claim” and triggers a transaction in Scroll network which calls “claim” function on bridge contract.
  - UI transmits to the bridge contract in Scroll Merkle proof of OP deposit and bridge parameters (asset, value, recipient).
  - Request OP state root from L1 with the help of L1SLOAD precompile.
  - Check of validity of Merkle proof for received root and  bridge parameters
  - Once check is successful, assets are transferred to recipient wallet in Scroll network.

