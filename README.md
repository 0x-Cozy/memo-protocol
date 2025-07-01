# Memo Protocol

> 🧪 Originally built for the [Sui Overflow Hackathon](https://sui.io/overflow), now maintained as a public utility by [@0x-Cozy](https://github.com/0x-Cozy).

![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen)

A protocol for attaching memos to Sui transactions, with both on-chain contracts and a TypeScript SDK.

## Contracts

The Memo Protocol contracts are deployed on Sui testnet. You can find the contract code in the `contracts/` directory.

### Contract Addresses

- Testnet: `0x21eba4a9ac6005260f45e776afebf02de42eada48438deceac0b76b9886e37d8`
- Mainnet: `0x` (TODO)

## SDK

A TypeScript SDK for interacting with the Memo Protocol.

### Installation

```bash
npm install memo-protocol-sdk
```

### Usage

```typescript
import { Transaction } from "@mysten/sui/transactions";
import { attachMemo, parseMemo, parseMemoFromTx, decodeMemoMessage } from "memo-protocol-sdk";

// Attach a memo to a transaction
const tx = new Transaction();
attachMemo(tx, "Hello World");

// Optionally specify a custom contract address if you've deployed your own
attachMemo(tx, "Hello World", { moduleAddress: "0x..." });

// Parse memos from a transaction response
const memos = parseMemoFromTx(txResponse);
const decodedMessages = memos.map(decodeMemoMessage);

// Parse a single memo event
const memo = parseMemo(event);
const message = decodeMemoMessage(memo);
```

### API Reference

#### `attachMemo(tx: Transaction, message: string, options?: { moduleAddress?: string })`
Attaches a memo message to a transaction. The message must be non-empty and less than 1024 bytes.
- `moduleAddress`: Optional address of your deployed memo contract

#### `parseMemo(event: SuiEvent): MemoEvent`
Parses a memo event from a Sui event object.

#### `parseMemoFromTx(tx: SuiTransactionBlockResponse): MemoEvent[]`
Parses all memo events from a transaction response.

#### `decodeMemoMessage(memo: MemoEvent): string`
Decodes the message bytes from a memo event into a string.

#### Note that memos are emitted as events so the option
`showEvents: true` is necessary.

## Project Structure

```
memo-protocol/
├── contracts/            # Smart contract code
├── memo-protocol-sdk/    # TypeScript SDK
│   ├── src/
│   │   ├── index.ts           # Main SDK implementation
│   │   ├── index.test.ts      # Unit tests
│   │   ├── live.test.ts       # Live network tests
│   │   └── test.script.ts     # Example usage script
│   ├── dist/                  # Compiled output
│   ├── package.json
│   ├── tsconfig.json
│   └── jest.config.js
└── README.md
```

## Development

### Building SDK

```bash
cd memo-protocol-sdk
npm run build
```

### Testing SDK

```bash
cd memo-protocol-sdk
npm test
```

### Running Example Script

```bash
cd memo-protocol-sdk
npx ts-node src/test.script.ts
```

## Contributing

Contributions are welcome! Feel free to open issues for bugs, feature requests, or improvements. Pull requests are appreciated - make sure to include tests and keep the code style consistent.

## License

MIT 
