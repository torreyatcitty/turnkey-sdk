# @turnkey/iframe-stamper

[![npm](https://img.shields.io/npm/v/@turnkey/iframe-stamper?color=%234C48FF)](https://www.npmjs.com/package/@turnkey/iframe-stamper)

This package contains functions to stamp a Turnkey request through credentials contained in an iframe. It is meant to be used with [`@turnkey/http`](https://www.npmjs.com/package/@turnkey/http) to build flows.

Usage:

```ts
import { IframeStamper } from "@turnkey/iframe-stamper";
import { TurnkeyClient } from "@turnkey/http";

const TurnkeyIframeContainerId = "turnkey-iframe-container";
const TurnkeyIframeElementId = "turnkey-iframe";

const iframeStamper = new IframeStamper({
  iframeUrl: process.env.IFRAME_URL!,
  iframeContainerId: TurnkeyIframeContainerId,
  iframeElementId: TurnkeyIframeElementId,
});

// This inserts the iframe in the DOM and returns the public key
const publicKey = await iframeStamper.init();

// Injects a new credential in the iframe
const injected = await iframeStamper.injectRecoveryBundle(recoveryBundle);

// New HTTP client able to sign with the credentials inside of the iframe
const httpClient = new TurnkeyClient(
  { baseUrl: "https://api.turnkey.com" },
  iframeStamper
);
```
