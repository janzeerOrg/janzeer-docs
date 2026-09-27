# Janzeer Glossary

Definitions of the terms used across the Janzeer documentation. Each entry shows the Arabic equivalent in
parentheses for cross-reference with the Arabic edition. Exact byte-level definitions live in the Yellow Paper.

## Core concepts

**Blockchain (سلسلة الكتل)** — An append-only ledger of blocks, each cryptographically linked to the previous one. Janzeer is a fixed-supply, permissionless, stake-free Layer-1.

**Block (الكتلة)** — A batch of transactions plus metadata (height, previous-block hash, producer public key, signature) committed to the ledger. Janzeer produces one main block per slot (15 seconds).

**Genesis block (الكتلة التكوينية)** — The first block(s) that bootstrap the chain and define the initial active validator set. Janzeer also produces a genesis block at each epoch boundary to re-elect the active set; it commits the epoch index, the privileged-anchor count, and the frozen active-validator keys.

**Main block (الكتلة الرئيسية)** — An ordinary block carrying user transactions and the resulting state, identified by transaction/state/receipt Merkle roots.

**Epoch (الحقبة / epoch)** — A span of 17,000 main blocks (≈ 3 days at 15-second blocks); at each epoch boundary the active validator set is re-elected.

**Slot (الفترة الزمنية / slot)** — A fixed 15-second window (12,000 ms active + 3,000 ms intermission) assigned round-robin to one validator who may produce that slot's block.

## Accounts & value

**Native coin (العملة الأصلية)** — Janzeer's unit of value. Fixed maximum supply of 100,000,000, never minted; amounts are tracked to 8 decimal places.

**Supply — maximum / circulating (المعروض الأقصى / المتداول)** — The hard cap (100,000,000) and the portion outside the treasury (`circulating = max − treasury balance`).

**Treasury / bank (الخزينة)** — The key-less genesis account `0x0000…0000` holding 77,500,000 pre-allocated coins that pay block rewards and receive the recycled fee share and registration deposits. No one can spend it directly; only protocol rules move it.

**Address (العنوان)** — A `0x`-prefixed, 20-byte identifier derived as the first 20 bytes of `keccak256(compressed public key)`. The canonical stored/hashed form is all-lowercase hex. (Not Ethereum-compatible — see the Yellow Paper.)

**EIP-55 checksum (تدقيق EIP-55)** — A display-only mixed-case rendering of an address (each hex letter is uppercased where its keccak nibble is ≥ 8), applied and validated at the wallet/API boundary. It is presentational, not consensus-relevant; all-lowercase input is always accepted.

**Wallet (المحفظة)** — Client-side software that derives keys from a recovery phrase and signs transactions. Janzeer wallets are non-custodial.

**HD wallet (المحفظة الهرمية الحتمية)** — A hierarchical-deterministic wallet: all keys derive from a single seed along the fixed path `m/0/0/0`, so one recovery phrase reproduces every key.

**Seed phrase / recovery phrase (عبارة الاسترداد)** — A 12- or 24-word mnemonic from which all your keys are derived. It is never stored by the network and cannot be recovered if lost.

**Public / private key (المفتاح العام / الخاص)** — The secp256k1 key pair derived at path `m/0/0/0`. The private key signs; the public key (compressed, 33 bytes) yields the address and verifies signatures.

**Nonce (الرقم التسلسلي / nonce)** — A per-account counter included in every transaction to order transactions and prevent replay.

## Transactions

**Transaction (المعاملة)** — A signed instruction submitted to the network. Janzeer has Transfer, Promoter, Exit-Promoter (user) and Reward, Slashing (system) types.

**TransferTx (معاملة التحويل)** — A transaction that moves coins between accounts, optionally carrying a memo (`data`, ≤ 256 bytes).

**PromoterTx (معاملة الترشُّح)** — A transaction that registers a node as a validator. It carries the 2000-coin registration deposit (to the treasury) and a fee of 3; there is no vote or approval.

**ExitPromoterTx (معاملة إنهاء الترشُّح)** — A transaction by which a validator gracefully retires. It removes the validator from the active set and slot schedule at the next epoch boundary. The registration deposit is not returned.

**Registration deposit (وديعة الترشُّح)** — The fixed 2000-coin amount a PromoterTx sends to the treasury to admit a validator. It is non-refundable and, together with one-seat-per-key, is the primary Sybil guard.

**Fee (الرسوم)** — The cost of a transaction. 80% goes to the block producer, 20% to the treasury (never burned). Minimums and exact per-type fees are defined in the Yellow Paper.

**Signature (التوقيع)** — An ECDSA (secp256k1, RFC-6979, low-S, DER, Base64) signature over the transaction's 32-byte hash, proving the sender authorized it.

**Hash (التجزئة / hash)** — A double-SHA256 digest (lowercase hex) identifying a transaction, block, or state entry.

**Merkle root (جذر ميركل)** — A single hash summarizing a set of items (transactions, state entries, receipts) so a block can commit to all of them compactly.

**Network ID (معرّف الشبكة)** — A per-chain string (default `janzeer`) bound into both the signed transaction preimage and the P2P handshake, so a transaction signed for one network cannot be replayed on another.

**Mempool (ذاكرة المعاملات المعلّقة / mempool)** — The pool of accepted-but-not-yet-confirmed transactions awaiting inclusion in a block.

## Native tokens (JZT-1)

**Native token / JZT-1 (الرمز الأصلي / JZT-1)** — A user-defined fungible token issued on Janzeer. It lives on a separate ledger from the native coin: a token's supply is not part of the coin's fixed 100,000,000 and does not touch emission, the treasury, or rewards. Every token operation still pays its fee in the native coin.

**TokenTx (معاملة الرمز)** — The single transaction type for all token operations. It carries an `op` byte selecting one of CREATE, MINT, BURN, SETCAP, or TRANSFER.

**Token id (مُعرِّف الرمز)** — The globally-unique identifier of a token, equal to its CREATE transaction hash. There is no symbol registry (symbols are not unique); the `tokenId` is.

**Issuer (المُصدِر)** — The validator that created a token. It is the only party allowed to mint, burn, or change that token's cap.

**Cap (السقف)** — A token's maximum supply. `totalSupply` is always kept within `0..cap`; a SETCAP operation cannot drop the cap below the already-minted supply.

**Mint / Burn (السكّ / الحرق)** — Issuer-only operations that increase (mint) or decrease (burn) a token's total supply, within the cap.

**Decimals (المنازل العشرية)** — Display-only precision for a token (0–18). It does not affect on-chain math; token amounts are stored as integer base units.

**Base units (الوحدات الأساسية)** — The integer on-chain representation of a token amount (like ERC-20 raw units); a displayed amount equals base units divided by `10^decimals`.

## Consensus

**Consensus (الإجماع)** — The rules by which nodes agree on the ledger. Janzeer uses permissionless validator block production in a fixed rotation with two-phase (PREPARE→COMMIT) BFT finality.

**Validator (المُصادِق)** — A registered node that produces and finalizes blocks. Nodes are admitted permissionlessly by submitting a PromoterTx with the non-refundable deposit — there are no votes and no approval. *Legacy name:* internally the code still calls a validator a "promoter" — the transaction TYPES (`PromoterTx`, `ExitPromoterTx`, `PromoterState`), the config keys (`promoters-count`, `fee-promoter-tx`, `amount-promoter-tx`), and the DB tables (`promoter_state`, `promoter_tx`, `exit_promoter_tx`, `genesis_promoter`) keep that original name, while the REST endpoints and JSON fields now use "validator"; a promoter is exactly a validator.

**Registration order (ترتيب الترشُّح)** — The election ordering: eligible validators are ranked by `createDate` (registration time), longest-registered first. This replaces the removed rating/vote-weight ordering.

**Active set (المجموعة النشطة)** — The validators eligible to produce and finalize blocks in the current epoch: still-privileged anchors plus the longest-registered elected validators, filled up to 21, minus offline/banned/exited nodes, with 5 rotating seats.

**Fair rotation (التناوب العادل)** — The mechanism by which the 5 rotating seats cycle round-robin through the standby candidate pool (up to 100) in registration order, giving overflow validators regular production turns.

**Proven independent validator (المُصادِق المستقل المُثبَت)** — A non-anchor validator that has produced blocks in every one of the last 2 epochs (`validator-proven-epochs`). Proven independents (not raw registrations) are what allow anchors to phase out.

**Anchor (المرساة)** — A founding validator defined in the epoch-1 genesis active set. Anchors start privileged (always-in, downtime-immune) but automatically phase out over time.

**Anchor phase-out (إلغاء تفعيل المراسي)** — The decentralization mechanism: anchors shed their privilege one per epoch (`anchor-demotions-per-epoch`) as proven independent validators come online, never dropping the healthy set below the safety floor. A demoted anchor keeps validating on merit like any registrant; if independents later collapse below the floor, dormant anchors re-engage. The privileged count is committed per epoch in the genesis block.

**Safety floor (الحد الأدنى للأمان)** — The minimum number of healthy validators (`safety-floor-validators = 4`) below which anchors will not phase out and dormant anchors re-engage.

**Reward / block reward / emission (المكافأة / مكافأة الكتلة / الإصدار)** — Coins paid from the treasury to a block's producing validator (100%, no commission or delegation split), following a declining schedule plus fee recycling (the "C+D" model). No new coins are minted.

**Quorum (النِّصاب)** — The vote threshold for finality: `floor(2N/3) + 1` of the N active validators (i.e. "2f+1").

**Finality (النهائية)** — The point at which a block is irreversible. Janzeer has single-block finality once a COMMIT quorum is reached.

**Equivocation (التصويت المزدوج)** — A validator signing two conflicting votes for the same slot and stage — a provable fault.

**Slashing (المصادرة / slashing)** — The penalty for equivocation: after 2 proven offenses a validator is permanently banned; the reporter receives a bounty.

**Ban (الحظر)** — Permanent removal of a repeat equivocator from validation; a banned validator can never rejoin the active set.

**Chain-spec digest (بصمة مواصفات السلسلة)** — A double-SHA256 digest over the genesis-pinned consensus parameters. Nodes exchange it in the handshake; a peer whose digest differs is rejected, so an operator who edits any consensus rule forks itself off the network.

## Network & operations

**Node (العقدة)** — Software that maintains the ledger, relays data, and (if it has a valid signing key) produces and votes on blocks.

**Peer (النظير)** — Another node a given node connects to over the P2P network.

**Network (الشبكة)** — The set of interconnected nodes. Janzeer peers communicate over an authenticated Netty TCP protocol.

**Non-custodial (غير حافظ للمفاتيح)** — A design in which only the user holds their keys and seed phrase; the network never sees or stores them and cannot move user funds.

**API endpoint (نقطة نهاية الواجهة البرمجية)** — A REST URL under `/api/v1/` exposed by a node for reading chain data and submitting transactions.

---

*Document status: v1.0 — reflects Janzeer node version 0.1.0. Byte-level definitions are authoritative in the Yellow Paper.*
