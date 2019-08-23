### Rascunho para lembretes da conclusão da API para integração com o frontend

1. Instalamos o modulo 'cors', ele permite que outras aplicações acessem a api e define quais endereços podem ser acessados

2. Em 'app.js'

```js
import cors from 'cors';
|
|
|
middlewares() {
    this.server.use(Sentry.Handlers.requestHandler());
    this.server.use(cors());
    this.server.use(express.json());
|
|
```
