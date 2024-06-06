# Email Wallet on Nibiru

A smart contract wallet controlled using emails.


Email Wallet is an Nibiru contract wallet that can be controlled by sending emails. The contract validates the authenticity of emails by verifying the ZK Proof of DKIM signature of the email. This ensures email is generated by the user without leaking user's email address on-chain.

#### Things you can do:

- ✓ Send Nibi to email address and Nibiru addresses.
  - `Send 1 Nibi to friend@domain.com`
  - `Send 2.5 Nibi to nibi1tsgl9sr8ayy4s9fdf9mr2ck2tptpjy2shdj7ky`

- ✓ Send CW20 to email address and Nibi addresses.
  - `Send 1.5 RHV to friend@skiff.com`
  - `Send 21.14 RHV to nibi1tsgl9sr8ayy4s9fdf9mr2ck2tptpjy2shdj7ky`

- ✓ Use NFT extension to mint NFTs.
  - `NFT Send 1 of FHM to recipient@domain.com` (and more)

- ✓ Execute any calldata on a target contract
  - `Execute nibi15qsut0gpr53h4.....`

### In progress:

- ✓ Install extensions for additional functionalities. Extensions can be developed for any DeFi protocols.
  - `Install extension Nibi-Swap`
  - `Remove extension Nibi-Swap`

- ✓ Use Nibi-Swap extension to swap tokens.
  - `Swap 1 UNIBI to FHM`
  - `Swap 1 FHM to UNIBI`
 
- ✓ Use account abstraction to be more privacy

- ✓ Set email wallet to a new owner. New owner (EOA) can control the wallet by executing any calldata on a target contract.
  - `Exit Email Wallet. Set owner to nibi1tsgl9sr8ayy4s9fdf9mr2ck2tptpjy2shdj7ky...`

#### Features:
- ✓ Easy send any tokens to other address via Gmail
- ✓ No need to install any browser extension or mobile app.
- ✓ No need to remember any seed phrase or private key.
- ✓ Operate the wallet by sending human readable emails.
- ✓ Hide link from an email address to a wallet address.
- ✓ Developers can build extensions to add new functionalities.

#### Security Considerations:
1. Safety guarantee: if your email domain server does not forge your emails, no one can send assets in your wallet.
2. Liveness guarantee: if your email domain server does not block your emails and you stores an invitation email that you have received before, you can execute a new transaction on-chain.
3. Privacy protection against DoS scanning attacks: no adversary can learn an address or existence of the wallet for your email address for free.
- Sender might be able learn the recipient's wallet address by scanning blockchain for the specific amount.



## Prerequisites
1. Technology Stack Selection
- Languages: Rust, TypeScript,
- Frameworks and Libraries: Nodejs, Nibidjs,
- Database: Postgres,
  
2. Development Environment
- Tools: Cosmwasm, Nibid CLI
- Testing tool: Jest

## Installation



## How it Works
Emails you send are (usually) signed using a private key controlled by your email domain server according to a DKIM protocol. This signature is included in the headers section of the email.

Email Wallet verify the DKIM signature of an email to ensure the mail was sent by the user and the contents are not forged. Instead of verifying the signature directly on-chain, a zk proof of signature is created (by a permissionless entity called Relayer) and verified on-chain.

Here is how a typical interaction with the wallet looks like:

- You send an email to Relayer's email address : "emailrelayer2003@gmail.com" with a subject like "Send 1 unibi to recipient@gmail.com".
- The Relayer verifies the DKIM signature and creates a zk proof of email.
- The ZK circuit extracts the subject, recipient email, timestamp, and other data from the email.
- Relayer calls the smart contract with the zk proof and the extracted data.
- Contract computes the subject from the extracted data and matches it with the subject passed by the Relayer.
- The ZK proof of email is validated on-chain, which also validates the subject.
- Private data like the sender email, recipient's email in the subject line, is not exposed on-chain.
- The smart contract executes the transaction and sends 1 unibi to recipient's Email Wallet address.
- The Relayer wait for the transaction confirmation, and send you and the recipient an email with the transaction details.


## How to Use
You send an email to Relayer's email address : "emailrelayer2003@gmail.com" with a subject like : "COMMAND to recipient@gmail.com".

Here are some COMMANDs, you can use:
- To send nibiru/custom cw20 to someone:

  `SEND <amount> <denom> to <recipient_mail_address>` 
  `Ex: Send 1 unibi to recipient@gmail.com` ||

   `Send 10 tf/nibi1ty88gpudfh57kqghy62hw8k4nt7765gczu2gqry5gl9ldurrzrns92scum/nubis to recipient@gmail.com`
- To send NFT/cw721 to someone:
  
  `SEND <NFT_Contract_address> <Token_id> to recipient@gmail.com`
  
  `Ex: Send nibi1jgpxjfetcgwnncms2dl0tt22dntnp0wtt28w6u5xeqqwfjh0p89spd40pr 5 to recipient@gmail.com`
* Note: Make sure you have enough tokens to send
