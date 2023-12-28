# EXAMPLE-OF-CONTROLLER-OF-EVENT-OMS-FEED

<!-- DOCS-IGNORE:start -->
<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->

[![All Contributors](https://img.shields.io/badge/all_contributors-1-orange.svg?style=flat-square)](#contributors-)

<!-- ALL-CONTRIBUTORS-BADGE:END -->
<!-- DOCS-IGNORE:end -->

Change language from README to [![es](https://img.shields.io/badge/lang-es-yellow.svg)](https://github.com/FelCer/orders-feed-example-node/blob/main/docs/README.md)

## Order Broadcast

A boilerplate app implementing an event handler receiving status updates from OMS Feed.
This is the method for using [Feed v3 Hook](https://developers.vtex.com/reference/feed-v3) inside VTEX IO.
<br>

## Implementation

1. Importar `{{vendor}}.testfelipe` en el archivo `manifest.json` del tema de IO.

```
  "dependencies": {
    // Validar la versión que se encuentra la aplicación.
    "{{vendor}}.testfelipe": "0.x",
  }
```

## example use

This app handles events sent by the app `vtex.orders-broadcast`, as you can see by looking at `node/service.json`.

```json
{
  "memory": 256,
  "ttl": 10,
  "timeout": 2,
  "minReplicas": 2,
  "maxReplicas": 4,
  "workers": 1,
  "events": {
    "allStates": {
      "sender": "vtex.orders-broadcast",
      "topics": ["order-status-updated"]
    },
    "someStates": {
      "sender": "vtex.orders-broadcast",
      "topics": ["cancel", "order-created"]
    }
  }
}
```

You have two ways of consuming changes in status:

1. Receive all events subscribing to the `order-status-updated` topic, as the `allStates` handler does
2. Receive a selection of status changes where the `currentState` equals the `topic`, as the `someStates` handler does. This option is the preferred one, when you know ahead of time, what types of events, you want to listen to.

Normally `vtex.orders-broadcast` sends events only in `master` workspace. If you want to use it in a developer workspace, do the following:

1. Create your development workspace by running `vtex use {workspaceName}`
2. Go to `https://{accountName}.myvtex.com/admin/apps/vtex.orders-broadcast/setup`
3. Change the `Target Workspace` variable to the name of the workspace you have created previously.
4. Now you can link this app (`vtex.orders-feed-example`) in your desired workspace and receive order status updates.

Here is an example body that you can expect to receive:

```json
{
  "recorder": {
    "_record": {
      "x-vtex-meta": {},
      "x-vtex-meta-bucket": {}
    }
  },
  "domain": "Marketplace",
  "orderId": "v69305315atmc-01",
  "currentState": "invoice",
  "lastState": "payment-approved",
  "currentChangeDate": "2020-07-13T20:25:13.2304508Z",
  "lastChangeDate": "2020-07-13T20:25:03.9527532Z"
}
```

If you want to understand further how Feed v3 works, check out [this documentation](https://help.vtex.com/tutorial/orders-management-feed-v3-setup--5qDml3cQypWDRTgw69s4C1).

## Contributors ✨

Thanks goes to these wonderful people: ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<table>
  <tr>
    <td align="center"><img src="https://avatars.githubusercontent.com/u/22477264?v=4" width="100px;" alt=""/><br /><sub><b>Luis Felipe Cerero Garcia</b></sub></a><br /><a href="https://github.com/FelCer/orders-feed-example-node/commits?author=felcer" title="Documentation">📖</td>
  </tr>
</table>

<!-- DOCS-IGNORE:end -->
