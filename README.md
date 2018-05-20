# NATS - Websocket Javascript Client

A websocket client for the [NATS messaging system](https://nats.io).

[![license](https://img.shields.io/github/license/nats-io/ws-nats.svg)](https://www.apache.org/licenses/LICENSE-2.0)
[![Travis branch](https://img.shields.io/travis/nats-io/ws-nats/master.svg)]()
[![Coveralls github branch](https://img.shields.io/coveralls/github/nats-io/ws-nats/master.svg)]()
[![npm](https://img.shields.io/npm/v/nats.svg)](https://www.npmjs.com/package/wsnats)
[![npm](https://img.shields.io/npm/dm/nats.svg)](https://www.npmjs.com/package/wsnats)

# Installation

```bash
npm install wsnats
```

Ws-nats requires a websocket proxy, if the NATS server requires LTS, the websocket must be a secure websocket.

# API

Ws-nats supports Promises, depending on the browser/runtime environment you can also use async-await constructs.

```typescript

import {NatsConnection, Msg} from 'wsnats';

async function test() {
let nc = await NatsConnection.connect({url: `ws://localhost:${PORT}`});

// publish a message
nc.publish('hello', 'nats');


// simple subscription
let sub = await nc.subscribe('hello', (msg: Msg) => {
    if (msg.reply) {
        nc.publish(msg.reply, `hi there ${msg.data}`);
    }
});

// simple request
let msg = await nc.requestOne('hello', 1000, 'nats request');

nc.close();

}
```

