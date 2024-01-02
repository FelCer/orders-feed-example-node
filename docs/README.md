# EJEMPLO-DE-CONTROLADOR-DE-EVENTOS-OMS-FEED

<!-- DOCS-IGNORE:start -->
<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->

[![All Contributors](https://img.shields.io/badge/all_contributors-1-orange.svg?style=flat-square)](#contributors-)

<!-- ALL-CONTRIBUTORS-BADGE:END -->
<!-- DOCS-IGNORE:end -->

Cambiar lenguaje de README a [![en](https://img.shields.io/badge/lang-en-red.svg)](https://github.com/FelCer/orders-feed-example-node/blob/main/docs/README.en.md)
## Order Broadcast

Una aplicación estándar que implementa un controlador de eventos que recibe actualizaciones de estado de OMS Feed.
Este es el método para usar [Feed v3 Hook](https://developers.vtex.com/reference/feed-v3) dentro de VTEX IO.
<br>

## Implementación

1. Importar `{{vendor}}.testfelipe` en el archivo `manifest.json` del tema de IO.

```
  "dependencies": {
    // Validar la versión que se encuentra la aplicación.
    "{{vendor}}.testfelipe": "0.x",
  }
```

## Ejemplo de uso

Esta aplicación maneja eventos enviados por la aplicación `vtex.orders-broadcast`, como puede ver al mirar `node/service.json`.

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

Tienes dos formas de consumir cambios de estado:

1. Reciba todos los eventos suscribiéndose al tema `order-status-updated`, como lo hace el controlador `allStates`
2. Reciba una selección de cambios de estado donde `currentState` sea igual a `topic`, como lo hace el controlador `someStates`. Esta opción es la preferida, cuando sabes de antemano qué tipos de eventos quieres escuchar.

Normalmente, `vtex.orders-broadcast` envía eventos solo en el espacio de trabajo `master`. Si desea utilizarlo en un espacio de trabajo de desarrollador, haga lo siguiente:

1. Cree su espacio de trabajo de desarrollo ejecutando `vtex use {workspaceName}`
2. Ir a `https://{accountName}.myvtex.com/admin/apps/vtex.orders-broadcast/setup`
3. Cambie la variable `Target Workspace` por el nombre del espacio de trabajo que ha creado anteriormente..
4. Ahora puede vincular esta aplicación (`vtex.orders-feed-example`) en el espacio de trabajo que desee y recibir actualizaciones del estado de los pedidos.

Aquí hay un cuerpo de ejemplo que puede esperar recibir:

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

Si desea comprender mejor cómo funciona Feed v3, consulte [esta documentación](https://help.vtex.com/tutorial/orders-management-feed-v3-setup--5qDml3cQypWDRTgw69s4C1).

<!-- DOCS-IGNORE:start -->

## Colaboradores ✨

Gracias a esta maravillosas persona: ([emoji key](https://allcontributors.org/docs/en/emoji-key)):

<table>
  <tr>
    <td align="center"><img src="https://avatars.githubusercontent.com/u/22477264?v=4" width="100px;" alt=""/><br /><sub><b>Luis Felipe Cerero Garcia</b></sub></a><br /><a href="https://github.com/FelCer/orders-feed-example-node/commits?author=felcer" title="Documentation">📖</td>
  </tr>
</table>

<!-- DOCS-IGNORE:end -->