# Janzeer User Guide

Welcome to Janzeer. Janzeer is a blockchain — a shared, tamper-resistant ledger of who owns what — with a fixed amount of coins and a wallet that is yours alone. This guide explains, in plain language, how to set up your wallet, send and receive coins, optionally run a validator to help secure the network, and stay safe. No technical background is needed; we explain each term the first time it appears.

## What Janzeer Is

Janzeer is a digital coin system. There is a **fixed supply** of coins — exactly **100,000,000** of them — and no new coins are ever created out of thin air. Every coin that will ever exist already exists; the network can only move them around, never print more. This is different from ordinary money, where a central bank can make more whenever it likes.

Janzeer is also **non-custodial**. This is the most important idea in this guide, so we'll say it plainly: **you, and only you, hold the keys to your coins.** A "key" is a secret that proves the coins are yours and lets you spend them. With Janzeer, that secret lives only in your wallet, on your own device. The network — the computers that run Janzeer — never sees it, never stores it, and can never use it. The flip side is that there is no "company" you can call to recover your account. You are your own bank. This guide will keep coming back to what that means for keeping your coins safe.

A quick note on names: in the software, the coin does not have a marketing ticker symbol. We simply call it **the coin** (sometimes "the native coin").

## Your Wallet

A **wallet** is the app that holds your keys and lets you send, receive, and manage your coins. Because Janzeer is non-custodial, the wallet does all the sensitive work on your own device.

### Creating a New Wallet

When you create a new wallet, it generates a **recovery phrase** — also called a **seed phrase** or **mnemonic**. This is a list of **12 ordinary English words** in a specific order, for example: `ribbon lake forest ...`. Those 12 words *are* your wallet. From them, your device can rebuild every key and address you own.

When you create your wallet you must:

1. **Write the 12 words down** on paper, in order, and keep them somewhere safe and private. Many people write two copies and store them in two separate safe places.
2. **Never type them into a website, share them, or take a photo of them.** Anyone who has your 12 words can take all your coins.
3. Understand that **the phrase cannot be recovered.** Nobody — not the Janzeer network, not the wallet makers, not any support desk — has a copy. If you lose the phrase and lose your device, the coins are gone for good.

This may feel strict, but it is the price of being truly in control of your own money: there is no third party who can lock you out, freeze your funds, or seize them — and likewise no third party who can rescue you if you lose your phrase.

### Restoring From a Recovery Phrase

If you get a new phone, lose your device, or want to use your wallet somewhere else, you can **restore** your wallet by entering the same 12 words, in the same order, into a fresh Janzeer wallet. The wallet rebuilds your keys and address exactly, and your balance reappears (the coins were never on the device — they live on the blockchain; the phrase just proves they're yours). This is why the phrase is so powerful, and why it must be protected so carefully.

### Your Password and Encrypted Vault

On a single device, typing 12 words every time would be tedious, so the wallet stores them for you in an **encrypted vault** — a locked container on your device — and protects it with a **password** you choose.

- The **password** unlocks the wallet on *this* device. It scrambles (encrypts) your stored phrase so that someone who picks up your phone can't read it.
- The **recovery phrase** is the master backup. If you forget your password or lose the device, the password won't help you — only the 12 words can bring your wallet back on a new device.

In short: the password protects day-to-day use; the recovery phrase is the true, ultimate backup. Choose a strong password, and still write the phrase down.

### Your Address

Your **address** is like an account number you share with others so they can send you coins. It looks like a string of letters and numbers beginning with `0x`, for example `0x06e1c0fa9955a700876f8cb0acc7f13fba9fb8ba`.

- It is safe to share your address publicly — it only lets people *send* you coins, never spend them.
- Your address is created from your keys, which come from your recovery phrase, so it always comes back when you restore your wallet.
- Your wallet displays the address in a **mixed-case** form (some letters upper, some lower), for example `0x06E1c0Fa9955a700876F8Cb0acc7F13fbA9fb8Ba`. This is a built-in **checksum** that helps catch typos. You can still paste an address in all-lowercase and it will be accepted — the mixed-case is only there to protect against mistyped characters.

## Sending and Receiving Coins

### Receiving

To receive coins, give the sender your **address** (above). When their transaction is confirmed, the coins appear in your balance. That's all you need to do.

### Sending

To send coins, your wallet asks you for two things:

1. **The recipient's address** — paste it carefully, or scan their QR code. Always double-check it; transactions cannot be reversed.
2. **The amount** to send. The smallest amount you can send is **0.1** coins. (Coins can be split very finely — down to 8 decimal places — but a normal transfer is at least 0.1.) The one exception: if you attach a **memo** (a short note, see below), you may send a smaller amount alongside it.

You'll also pay a small **fee** (see below). The wallet builds the transaction, signs it with your key *on your device*, and sends it to the network. You never reveal your key in the process — the network only receives proof that you authorized the payment.

### The Fee

Every transaction includes a small **fee** that helps run the network and reward the people who produce blocks. The **minimum fee is 0.01** coins. Most transfers use the minimum.

### What "Confirmed" Means

After you send, the network gathers transactions into a **block** — a batch of transactions agreed on by the network — and adds it to the chain. Janzeer has **single-block finality**: once your transaction is in a block that the network agrees on, it is **final and irreversible**. There is no waiting for "more confirmations" as on some other blockchains; one block is enough. When your wallet shows the transaction as **confirmed**, it's done.

### If a Transfer Stays Pending — Speed Up

A transfer normally confirms in well under a minute. If the network is busy, or a transfer was sent with a fee that is too low, it can wait in the queue — your wallet lists it under **Pending**, and the amount is held (it is not spendable, but it has not left your account either). While it waits, your later transfers wait behind it.

You have two choices:

- **Wait.** A transfer that is not confirmed within **six hours** is dropped by the network by itself; the held amount becomes spendable again and nothing was charged.
- **Speed up.** Open the pending transfer and choose **Speed up**. The wallet signs the *same* transfer again — same recipient, same amount, same memo — with a **higher fee** that you choose (it suggests double the old fee). The network keeps whichever version pays more and discards the other, so **you pay only the new fee, never both**. Speed up cannot change the recipient or the amount, and it cannot cancel a transfer that has already been confirmed.

The minimum fee (0.01 JNZ) is enough whenever the network is not congested; a higher fee only matters when many transfers compete for the same block.

### Reading Your Balance

Your **balance** is the amount of coins you can spend right now. Your wallet shows it for you. A couple of things to know:

- Coins you've just sent but that aren't confirmed yet are already set aside, so your spendable balance reflects what's truly available.
- Your wallet also shows your **nonce** — a simple counter of how many transactions you've sent. You don't need to manage it; the wallet uses it automatically to keep your transactions in order and to stop anyone from replaying an old payment.

## Tokens

Besides the native coin, Janzeer lets people create their own **tokens**. A token is a custom coin — with its own name and symbol — that anyone can hold and send, just like the native coin. Tokens live on the *same* blockchain as the native coin, but they are completely **separate** from it.

The most important thing to understand is this: **a token has its own supply, unrelated to the native coin.** Creating a token, or making more of it, never creates any native coins. The fixed supply of **100,000,000** native coins is untouched — a token is simply its own thing, tracked on the same ledger.

### Holding and Sending Tokens

You don't need to be anyone special to use tokens. **Anyone can receive and send a token they hold**, exactly the way you receive and send the native coin. If someone sends you a token, it appears in your wallet, and you can send it on to any address.

### Creating a Token

Creating a *new* token is the one thing an ordinary user can't do: **only a validator** (a registered node operator — see "Running a Validator" below) can create a token. When they do, they choose:

- a **symbol** (a short ticker, like `GOLD`) and a **name**,
- how many **decimal places** the token can be split into,
- a **maximum supply** (a cap the token can never exceed), and
- an optional **starting amount** to create for themselves right away.

### What You Can Do With Tokens

There are five token actions. Who can do each one depends on the action:

| Action | What it does | Who can do it |
|---|---|---|
| **Create** | Make a brand-new token (set its symbol, name, decimals, and max supply) | **Validators only** |
| **Mint** | Make more of an existing token (up to its cap) | Only the token's **creator** |
| **Burn** | Permanently destroy some of a token | Only the token's **creator** |
| **Change cap** | Adjust a token's maximum supply | Only the token's **creator** |
| **Transfer** | Send tokens you hold to another address | **Anyone** holding a balance |

In short: only a validator can *create* a token, and only that creator can *mint*, *burn*, or *change the cap* of their own token — but *anyone* who holds some of a token can *send* it.

### Token Fees

Every token action still pays its **fee in the native coin** (never in the token itself). The fees are:

- **Creating** a token costs **5** coins.
- **Minting, burning, changing the cap, or transferring** a token costs **0.01** coins each.

Your wallet always shows you the exact fee before you confirm an action.

### Tokens in Your Wallet

Your wallet has a **Tokens** tab. There you'll see all your balances in one place — your native coin *and* each token you hold — along with a simple form where you pick an action (such as Transfer) and fill in the details. After you confirm an action, the wallet **refreshes on its own** once the transaction is confirmed on the network, usually a block or two later, so your new balances appear without you having to do anything.

## Running a Validator

Janzeer is kept running by participants called **validators**. These are the computers (run by people or organizations) that take turns producing blocks and confirming everyone's transactions. There is no voting, no delegation, and no staking: you cannot "lend" your coins to a validator to earn a share of its rewards. Rewards are payment for the *work* of running the network, and they go **100% to the validator that produced the block**. If you simply hold coins, you never need to think about validators at all — this section is only for holders who want to run one.

### How to Become a Validator

Becoming a validator is **permissionless** — nobody has to approve you and there is no election to win. You need two things:

1. **Run a Janzeer node.** This is the software that produces and validates blocks. Setting one up is a technical task; see the Operator Guide for full instructions.
2. **Register it** by sending a **registration transaction** (a "validator" transaction) from your wallet. Registration alone admits you — there are no votes to collect.

Registration has a specific cost:

- A **fee of 3** coins (the fixed fee for a registration transaction).
- A **deposit of 2000** coins that goes to the network treasury and is **non-refundable**. This deposit is what keeps the validator set honest and hard to flood with fake identities — it is the price of a seat, not a stake you get back.

Be sure you understand that the 2000 deposit is **gone for good** the moment you register. It is not returned when you stop validating.

### How You Earn as a Validator

When it is your validator's turn and it produces a block, your validator's wallet receives that block's reward in full, plus a share of the fees from the transactions in that block. There is no commission to split and no delegators to pay — the producing validator keeps everything. You earn by doing the work of keeping the chain live, not by locking up coins.

### Stepping Down (Exit)

If you want to stop validating, you send an **exit transaction** to retire your validator gracefully. It is removed from the active line-up at the next scheduled changeover, so it cleanly stops being assigned turns. Exiting costs the usual minimum fee of **0.01**. Note again: exiting does **not** return your 2000 deposit — that is non-refundable by design.

> In plain terms: running a validator is a job, not an investment product. You put up a non-refundable deposit, run reliable hardware, and get paid for the blocks you produce. There is no way to earn simply by holding or "delegating" coins.

## Fees and Limits at a Glance

| Thing | Value | Plain meaning |
|---|---|---|
| Maximum coin supply | **100,000,000** | The total that will ever exist; never increased. |
| Minimum amount to send | **0.1** | The smallest normal transfer (smaller allowed if you attach a memo). |
| Minimum fee | **0.01** | The smallest fee on a transaction. |
| Validator registration fee | **3** | The fee to register a node as a validator. |
| Validator deposit | **2000** | Paid to the treasury on registration; **non-refundable**. |
| Token creation fee | **5** | The fee to create a new token (validators only); paid in the native coin. |
| Token action fee (mint/burn/change cap/transfer) | **0.01** | The fee for any other token action; paid in the native coin. |
| Optional memo (note) | up to **256 bytes** | A short note you may attach to a transfer. |

A **memo** is an optional short note (up to 256 bytes — roughly 256 characters) you can attach to a transfer, for example a reference or a thank-you. It's entirely optional.

## Security and Safety

Being your own bank is powerful, but it means safety is in your hands. A few rules will keep you protected:

- **Guard your recovery phrase above all else.** Those 12 words are full control of your coins. Keep them offline, on paper, in a safe place. Never store them in a screenshot, email, cloud note, or chat.
- **The network cannot recover your phrase.** There is no "forgot my password" for the phrase. If it's lost along with your device, the coins are unrecoverable. Back it up before you put real value in your wallet.
- **No one legitimate will ever ask for your phrase.** Not support staff, not an "airdrop," not a giveaway, not a wallet "verification." Anyone asking is trying to steal from you. Walk away.
- **Double-check addresses before sending.** Transactions are final and irreversible. Paste, then verify the first and last characters; scan a QR code when you can.
- **Use a strong wallet password** and keep your device and wallet app up to date.
- **Remember the wallet is non-custodial:** the network verifies that you signed a transaction, but it never holds your keys. Your security choices are what protect you.

## Frequently Asked Questions

**"Transaction timestamp is in the future" — what does that mean?** Your phone or computer clock is wrong. Every transaction carries the time it was signed, and the network only accepts times close to real time (up to a minute ahead, up to six hours old). Turn on automatic date and time on your device and send again. The six hours are only a safety margin for a transaction that waits in the queue; a normal transaction is confirmed in well under a minute.

**Is the coin supply really fixed?**
Yes. The maximum supply is **100,000,000** coins, and no new coins are ever minted. Block rewards are paid out of a pre-funded treasury that was set aside when the network started — they are *moved*, not created. So the total never grows.

**Can the network freeze or seize my coins?**
No. Janzeer is non-custodial: your keys live only on your device. The network can verify your transactions but cannot move, freeze, or take your coins. There is no central party with that power — which is exactly why protecting your own recovery phrase matters so much.

**What happens if I lose my recovery phrase?**
If you still have your wallet open and working on your device, restore access on a new device by writing the phrase down now while you can. If the phrase is lost *and* you lose access to the device, the coins cannot be recovered by anyone. Always keep a safe, offline backup of the 12 words.

**What is a validator?**
A validator is a participant whose computer helps run the network by taking turns producing blocks. Anyone can become one by running a node and registering it; there is no election or approval. The validator that produces a block keeps 100% of that block's reward.

**Can I earn by delegating or staking my coins?**
No. Janzeer has no delegation, staking, or voting. There is no way to lend your coins to a validator for a share of its rewards, and there are no rewards to "claim." The only way to earn network rewards is to run a validator yourself (see "Running a Validator"), which requires a node and a non-refundable 2000 deposit.

**How long until my payment is final?**
Janzeer has single-block finality. Once your transaction is included in a block the network agrees on, it is final and irreversible — there's no need to wait for extra confirmations.

**Why can't I just reset my password if I forget the phrase?**
Your password only unlocks the wallet on the device where you set it. The recovery phrase is the real master key. A forgotten password can be worked around *only* by restoring from the phrase on a fresh wallet — so the phrase is what you must never lose.

**Can I make my own token?**
Only if you run a validator. Creating a token requires being a registered node operator, and costs a **5**-coin fee. But you don't need to be a validator to *use* tokens — anyone can receive and send tokens they hold. A token has its own separate supply and never affects the fixed supply of native coins.

**Is it safe to share my address?**
Yes. Your address (`0x...`) only lets people send coins to you. It can never be used to spend your coins or access your wallet.

---

Document status: version 1.0. This guide reflects Janzeer node version 0.1.0. Exact byte-level and protocol details live in the Yellow Paper.
