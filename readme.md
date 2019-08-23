# Módulo 3 no Bootcamp da Rocketseat

Este é o Backend de uma aplicação desenvolvida chamada MeetApp durante o Bootcamp da Roketseat.

### Inicialização do projeto

- Para os que desejam rodar o projeto em sua máquina, basta seguir os passos abaixo e realizar os testes
- Requisitos:
  - Node/NPM
  - Yarn
  - Docker

1. Instânciamos o banco de dados 'postgres' com o 'docker', passando o 'name' como 'database' e o 'password' como 'docker' na porta 5432.

   - Executando pela primeira vez, utilizamos o comando 'run' para criar o container do 'postgres'
     > docker run --name database -e POSTGRES_PASSWORD=docker -p 5432:5432 -d postgres
   - A partir da segunda vez, basta startar o servidor
     > docker start database

- Feito isso, podemos baixar o programa 'PostBird' para vacilitar a visualização dos dados. Após baixado, acessamos com o nome e a senha que foram criadas na imagem do postgress, e criamos um novo database com o nome 'gobarber'

2. Instânciamos uma imagem do mongodb com o nome 'mongobarber', para trabalharmos com dados não-relacionais

- Executando pela primeira vez, utilizamos o comando 'run' para criar o container do 'mongo'

  > docker run --name mongobarber -p 27017:27017 -d -t mongo

- A partir da segunda vez, basta startar o servidor

  > docker start mongobarber

- Instalamos o programa 'Mongo Compass' para utilizar como interface gráfica. Neste caso não precisamos criar a base de dados pois ele vai ser criado automaticamente.

3. Instânciamos também o 'redis' para utilizar as filas no envio de email

   - Executando pela primeira vez, utilizamos o comando 'run' para criar o container do 'redis'
     > docker run --name redisgobarber -p 6379:6379 -d -t redis:alpine
   - Executando pela segunda vez
     > docker start redisgobarber

4. Rodamos o comando yarn para fazer a instalação das dependências passadas no 'package.json'

   > yarn

5. Executamos as 'migrations' para criar as tabelas no banco de dados

   > yarn sequelize db:migrate

6. Rodamos a aplicação da api

   > yarn dev

7. Rodamos a aplição da fila

   > yarn queue
