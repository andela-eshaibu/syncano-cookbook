# Middleware settings

## Install socket
```sh
$ s add middleware-socket
```
## How to use

```js
import Server from 'syncano-server'
let middleware = {
  // any socket that follows the rules of middleware
  parallel: ['validator/validate','token-middleware/check-token-middleware']
}
export default async ctx => {
  const {data, response, socket} = Server(ctx)
  try {
    await socket.post('middleware-socket/execute', {
      middleware,
      args: ctx.args,
      meta: ctx.meta
    })
    return response.json({})
  } catch (e) {
    let {message} = e
    let status = 400
    if (e.response) {
      let {status, data: message} = e.response
    }
    return response.json(message, status)
  }
}
```