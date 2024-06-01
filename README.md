# sockittt

A sweet little WebSocket client for the browser and other `WebSocket`-compatible runtimes

## Installation

```bash
yarn add sockittt
```

## Usage

```typescript
import { Sockittt } from "sockittt";

const ws = new Sockittt("ws://localhost:8080", {
	onMessage: message => {
		console.log("Received:", message);
	},
	// Call .open() to immediately open the connection
}).open();

ws.send("Hello, world!");
```
