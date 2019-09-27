<h1 align="center">
<img src="src/assets/logo.svg" width="180"/>

<br />
<br />
Gobarber Backend
</h1>

<p align="center">
  <a href="#tecnologias-utilizadas">Tecnologias utilizadas</a> |
  <a href="#como-usar">Como Usar</a> |
  <a href="#rotas">Rotas</a>
</p>

Este é o backend de um projeto criado durante os módulos 8, 9 e 10 no Bootcamp da Rocketseat. Nele desenvolvemos um serviço apelidado de GoBarber onde os usuários podem se cadastrar como prestador de serviços na [aplicação web](https://github.com/rodrigodasilva/gobarber-front-web) feita em ReactJS, e outros usuários podem agendar horário com estes prestadores através do [aplicativo](https://github.com/rodrigodasilva/gobarber-mobile) desenvolvido em React-native, sendo toda a lógica gerenciada por esta api desenvolvida em NodeJS.

## Tecnologias utilizadas

- [sentry/node](https://github.com/getsentry/sentry-javascript/tree/master/packages/node)
- [bcryptjs](https://github.com/dcodeIO/bcrypt.js/blob/master/README.md)
- [bee-queue](https://github.com/bee-queue/bee-queue)
- [cors](https://github.com/expressjs/cors)
- [date-fns](https://github.com/date-fns/date-fns)
- [dotenv](https://github.com/motdotla/dotenv)
- [express](https://github.com/expressjs/express)
- [express-async-errors](https://github.com/davidbanham/express-async-errors)
- [express-handlebars](https://github.com/ericf/express-handlebars)
- [jsonwebtoken](https://github.com/auth0/node-jsonwebtoken)
- [mongoose](https://github.com/Automattic/mongoose)
- [multer](https://github.com/expressjs/multer)
- [nodemailer](https://github.com/nodemailer/nodemailer)
- [nodemailer-express-handlebars](https://github.com/yads/nodemailer-express-handlebars)
- [pg](https://github.com/brianc/node-postgres)
- [pg-hstore](https://github.com/scarney81/pg-hstore)
- [sequelize](https://github.com/sequelize/sequelize)
- [sequelize-cli](https://github.com/sequelize/cli)
- [youch](https://github.com/poppinss/youch)
- [yup](https://github.com/jquense/yup)

## Como usar

#### Pré-requisitos:

Ferramentas

- Yarn/Npm
- Docker

Serviços

- Postgres
- Redis
- Mongodb

#### Configurando as variavéis de ambiente

1. Renomeamos o arquivo '.env_example' para '.env' e substituimos as informações de configuração conforme explicado nos passos seguintes

2. Definimos uma chave secreta para a aplicação

```
APP_SECRET=
```

3. É necessário ter uma instância do banco de dados postgres rodando e, a partir dela criar uma base de dados, adicionando então, estes dados ao arquivo de configuração

```
# Database
DB_HOST=
DB_USER=
DB_PASS=
DB_NAME=
```

4. Devemos instânciar também o redis e o mongodb, e alterar os dados no arquivo .env

```
MONGO_URL=

REDIS_HOST=127.0.0.1
REDIS_PORT=6379
```

5. Para simularmos o envio de emails utilizamos o serviço [mailtrap.io](https://mailtrap.io), logo, sugerimos que crie sua conta e substitua os dados fornecidos por eles nas linhas abaixo do arquivo .env

```
MAIL_HOST=
MAIL_PORT=
MAIL_USER=
MAIL_PASS=
```

#### Iniciado a aplicação

Depois de configurada as variavéis de ambiente e, tendo o postgres, o mongodb e o redis rodando podemos iniciar a api

1. Rodamos o comando yarn para fazer a instalação das dependências passadas no package.json

   > yarn

2. Executamos as migrations para criar as tabelas no banco de dados

   > yarn sequelize db:migrate

3. Rodamos a aplicação da api

   > yarn dev

4. Rodamos a aplição da fila

   > yarn queue

### Rotas

Se tudo ocorreu bem até aqui significa que a api está rodando, sendo assim podemos testar suas funcionalidades. Os tópicos seguintes descrevem as rotas fornecidas pela api e detalha como realizar a requisição de cada uma delas.

#### User

- Create

```json
/** Requisição
 * - Tipo: POST
 * - Rota: /users
 * - Body:
 *   > name: string
 *   > email: email
 *   > password: string de mínimo 6 caracteres
 **/

// Ex. de requisição
{
  "name": "João",
  "email": "joao@teste.com.br",
  "password": "123456"
}
```

- Update (necessário ter iniciado a sessão antes)

```json
/** Requisição
 * - Tipo: PUT
 * - Rota: /users
 * - Body:
 *   > name: string
 *   > email: email
 *   > oldPassword: string de mínimo 6 caracteres
 *   > password: string de mínimo 6 caracteres
 *   > confirmPassword: string de mínimo 6 caracteres
 **/

// Ex. de requisição
{
  "name": "João Teste",
  "email": "joao@teste.com",
  "oldPassword": "123456",
  "password": "1234567",
  "confirmPassword": "1234567"
}
```

#### Session

- Create

```json
/** Requisição
 * - Tipo: POST
 * - Rota: /sessions
 * - Body:
 *   > email
 *   > password
 **/

// Ex. de requisição
{
  "email": "joao@teste.com",
  "password": "123456"
}
```

Todas as rotas a partir daqui requerem **autenticação na sessão** e a inserção do token gerado no campo 'auth' do cabeçalho da mensagem

#### Files

- Create

```json

/** Requisição
 * - Tipo: POST
 * - Rota: /files
 * - Body:
 *   > file: arquivo (tipo multipart form)
 **/
```

#### Providers

- Index: lista todos provedores de serviços

```json
/** Requisição
 * - Tipo: GET
 * - Rota: /providers
 **/

// Ex. de requisição
"http://localhost:3333/providers"
```

- Index Available: lista os horários disponíveis de um prestador de serviço

```json
/** Requisição
 * - Tipo: GET
 * - Rota: /providers/:providerId/available
 * - Params:
 *   > id: number (id do prestador)
 **/

// Ex. de requisição
"http://localhost:3333/providers/2/available"
```

#### Appointments

- Index: lista os agendamentos que o usuário tem

```json
/** Requisição
 * - Tipo: GET
 * - Rota: /appointments
 * - Query params:
 *   > page: opcional
 **/

// Ex. de requisição
"http://localhost:3333/appointments"
```

- Create: cria um novo agendamento

```json
/** Requisição
 * - Tipo: POST
 * - Rota: /appointments/:id
 * - Params:
 *   > provider_id: number
 *   > date: date (formato ISO "YYYY-MM-DDTHH:mm:ss.sssZ")
 **/

// Ex. de requisição
"http://localhost:3333/appointments/2"
```

- Delete: deleta um agendamento

```json
/** Requisição
 * - Tipo: DELETE
 * - Rota: /appointments
 * - Params:
 *   > id: number (id do prestador)
 **/

// Ex. de requisição
"http://localhost:3333/appointments/2"
```

#### Schedule

- Index: lista os agendamentos que o prestador tem no dia

```json
/** Requisição
 * - Tipo: GET
 * - Rota: /schedule
 **/

// Ex. de requisição
"http://localhost:3333/schedule"
```

#### Notifications

- Index: lista as notificações recebidas pelo prestador de serviço

```json
/** Requisição
 * - Tipo: GET
 * - Rota: /notifications
 **/

// Ex. de requisição
"http://localhost:3333/notifications"
```

- Update: atualiza o estado das notificações do prestador

```json
/** Requisição
 * - Tipo: PUT
 * - Rota: /notifications/:id
 * - Params:
 *  > id: number (id da notificação)
 **/

// Ex. de requisição
"http://localhost:3333/notifications/3"
```
