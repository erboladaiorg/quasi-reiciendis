[![npm version](https://badge.fury.io/js/@erboladaiorg/quasi-reiciendis.svg)](https://badge.fury.io/js/@erboladaiorg/quasi-reiciendis)

# Resilient Websockets

- automatic retries when the message cannot be sent (e.g. when the connection is lost)
- ping/pong to keep the connection alive

## Installation

```bash
npm install @erboladaiorg/quasi-reiciendis
```

OR

```bash
yarn add @erboladaiorg/quasi-reiciendis
```

OR

```bash
pnpm add @erboladaiorg/quasi-reiciendis
```

## Usage

```js
import { ResilientWS } from '@erboladaiorg/quasi-reiciendis'

ResilientWS.create({
  url: '',
  onConnectCallback: () => {
    console.log(`Wow this is a websocket connection!`)
  },
  onDisconnectCallback: () => {
    console.log(`Wow this is a websocket disconnection!`)
  },
  onMessageCallback: (message) => {
    console.log(`Wow this is a websocket message!`, message)
  },
  onErrorCallback: (error) => {
    console.log(`Wow this is a websocket error!`, error)
  },
})
```

ResilientWS maintains a single instance. So you can import it anywhere and use it.

```js
import { ResilientWS } from '@erboladaiorg/quasi-reiciendis'

const ws = ResilientWS.getInstance()

ws.send({
    message: 'Hello World!'
    attempt: 0,
    forceReconnect: false,
})
```

### Ping/Pong

By default, ping/pong is disabled. You can enable it by passing the config for ping/pong when creating your ResilientWS instance.

```js
import { ResilientWS } from '@erboladaiorg/quasi-reiciendis'

ResilientWS.create({
  ...config,
  pingPongSettings: {
    enabled: true
    pingInterval: 10000,
    pingMessage: 'ping',
  },
})
```
