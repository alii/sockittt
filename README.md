# sockittt

A sweet little WebSocket client for the browser and other `WebSocket`-compatible runtimes

## Installation

```bash
yarn add sockittt
```

## Usage

```typescript
import { Sockittt } from "sockittt";

const subscriptions = new Set<(event: MessageEvent) => void>();

const ws = new Sockittt("ws://localhost:8080", {
	onMessage: message => {
		for (const subscription of subscriptions) {
			subscription(message);
		}
	},
}).open(); // Call .open() to immediately open the connection, this returns the instance

subscriptions.add(event => {
	console.log("Received", event.data);
});

ws.send("Hello, world!");
```

## Advanced usage

```typescript
import { Sockittt } from "sockittt";

const ws = new Sockittt("ws://localhost:8080", {
	timeout: 5000,
	maxAttempts: 10,
	onMessage: message => {
		console.log("Received", message.data);
	},
	onOpen: () => {
		console.log("Connected!");
	},
	onClose: () => {
		console.log("Disconnected!");
	},
	onReconnect: () => {
		console.log("Reconnecting...");
	},
	onDidExhaustMaxAttempts: () => {
		console.log("Reconnection attempts exceeded maxAttempts");
	},
	onError: error => {
		console.error("Error", error);
	},
	with: ws => {
		ws.binaryType = "arraybuffer";
	},
}).open();
```
