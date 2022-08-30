# Deviews Api

Essa é a API da Deviews

## **Endpoints**

A API tem um total de 5 endpoints, sendo em volta principalmente do usuário - podendo cadastrar seu perfil, fazer login, fazer posts e dar like em outros posts.

O url base da API é https://movies-server-kenzie.herokuapp.com/

## Rotas que não precisam de autenticação

### Cadastro

POST /register <br/>

Esse endpoint irá cadastrar o usuário, sendo que os campos obrigatórios são os de email, password, name, nickname, bio, techs.
Você pode ficar a vontade para adicionar qualquer outra propriedade no corpo do cadastro dos usuários.

`POST /register - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "frederico@mail.com",
  "password": "123456",
  "name": "Frederico",
  "nickname": "FredericoCãoDev",
  "bio": "Eu sou um pug dev!",
  "techs": ["Javascript", "React"]
}
```

Caso dê tudo certo, a resposta será assim:

`POST /register - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImZyZWRlcmljb0BtYWlsLmNvbSIsImlhdCI6MTY2MTg4ODAyNCwiZXhwIjoxNjYxODkxNjI0LCJzdWIiOiIxIn0.0WUbQsax-l6OI70W_cnfBD60Auq82rE2XjlMxaYkzCE",
  "user": {
    "email": "frederico@mail.com",
    "name": "Frederico",
    "nickname": "FredericoCãoDev",
    "bio": "Eu sou um pug dev!",
    "techs": ["Javascript", "React"],
    "id": 1
  }
}
```

### Login

POST /login <br/>

Esse endpoint é usado para realizar login com um dos usuários cadastrado.

`POST /login - FORMATO DA REQUISIÇÃO`

```json
{
  "email": "frederico@mail.com",
  "password": "123456"
}
```

Caso dê tudo certo, a resposta será assim:

`POST /login - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "accessToken": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6ImZyZWRlcmljb0BtYWlsLmNvbSIsImlhdCI6MTY2MTg4ODA4OSwiZXhwIjoxNjYxODkxNjg5LCJzdWIiOiIxIn0    RyeCQrvZ23R4IOWfjzSG7gC60Wjy7CEFbt3VPi5-iGk",
  "user": {
    "email": "frederico@mail.com",
    "name": "Frederico",
    "nickname": "FredericoCãoDev",
    "bio": "Eu sou um pug dev!",
    "techs": ["Javascript", "React"],
    "id": 1
  }
}
```

Com essa resposta, vemos que temos duas informações, o user e o token respectivo, dessa forma você pode guardar o token e o usuário logado no localStorage para fazer a gestão do usuário no seu frontend.

## Rotas que necessitam de autorização

Rotas que necessitam de autorização deve ser informado no cabeçalho da requisição o campo "Authorization", dessa forma:

> Authorization: Bearer {token}

Após o usuário estar logado, ele deve conseguir fazer novas postagens, editar os posts, deletar os posts, editar o perfil e deletar o perfil.

<h2 align ='center'> Criar um novo post </h2>

`POST /posts - FORMATO DA REQUISIÇÃO`

```json
{
  "content": "Meu primeiro post",
  "img": "https://ichef.bbci.co.uk/news/976/cpsprodpb/17638/production/_124800859_gettyimages-817514614.jpg",
  "userId": 1,
  "date": "30/08/2022",
  "response": [],
  "like": 0
}
```

O campo userId deve receber o Id do usuario

`POST /posts - FORMATO DA RESPOSTA - STATUS 201`

```json
{
  "content": "Meu primeiro post",
  "img": "https://ichef.bbci.co.uk/news/976/cpsprodpb/17638/production/_124800859_gettyimages-817514614.jpg",
  "userId": 1,
  "date": "30/08/2022",
  "id": 1
}
```

<h2 align ='center'> Editar um post </h2>

`PATCH /posts/:post_id - FORMATO DA REQUISIÇÃO`

```json
{
  "content": "Meu segundo post",
  "date": "30/08/2022"
}
```

`PATCH /posts/:post_id - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "content": "Meu segundo post",
  "img": "https://ichef.bbci.co.uk/news/976/cpsprodpb/17638/production/_124800859_gettyimages-817514614.jpg",
  "userId": 1,
  "date": "30/08/2022",
  "id": 1
}
```

<h2 align ='center'> Deletar um post </h2>

`DELETE /posts/:post_id - FORMATO DA REQUISIÇÃO`

```json
Não é necessário um corpo da requisição.
```

<h2 align ='center'> Editar perfil</h2>

`PATCH /users/:user_id - FORMATO DA REQUISIÇÃO`

```json
{
  "name": "Frederico II",
  "bio": "Eu sou um cão dev!",
  "techs": ["Javascript", "React", "Node"]
}
```

`PATCH /users/:user_id - FORMATO DA RESPOSTA - STATUS 200`

```json
{
  "email": "frederico@mail.com",
  "password": "$2a$10$MWgi3MwcbgSfZIYjefsaPuGRgmJoechcArpU2qkOkA8FCjsbcDdVa",
  "name": "Frederico II",
  "nickname": "FredericoCãoDev",
  "bio": "Eu sou um cão dev!",
  "techs": ["Javascript", "React", "Node"],
  "id": 1
}
```

<h2 align ='center'> Deletar perfil</h2>

`DELETE /users/:user_id - FORMATO DA REQUISIÇÃO`

```json
Não é necessário um corpo da requisição.
```
