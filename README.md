# frontend

## Project setup
```
npm install
```

### Compiles and hot-reloads for development
```
npm run serve
```

### Compiles and minifies for production
```
npm run build
```

### Run your tests
```
npm run test
```

### Lints and fixes files
```
npm run lint
```

### Customize configuration
See [Configuration Reference](https://cli.vuejs.org/config/).

src <br>
│   app.js          # Classe app <br>
│   server.js       # Server para iniciar o app <br>
└api              <br>
&nbsp;&nbsp;&nbsp; └─controllers   # Funções da controllers do express route <br>
&nbsp;&nbsp;&nbsp; └─models        # Modelos do banco de dados <br>
&nbsp;&nbsp;&nbsp; └─services      # Regras de negócio <br>
&nbsp;&nbsp;&nbsp; └─subscribers   # Eventos async  <br>
&nbsp;&nbsp;&nbsp; └─repositories* # Query builders  <br>
└config          # Configuração das variaveis de ambiente <br>
└jobs            # Tarefas de rotinas <br>
└loaders         # Modulos para utilizado no app <br>
└utils           # Trechos de código pequeno <br>
└helpers         # Trechos de arquitetura de código <br>
└routes          # Definição de rotas express <br>
└types           # Tipagem (d.ts) para Typescript <br>

# API Aster Cards

> Esta **API** é utilizada para conseguir realizar: 
## Register Page
>> - [x] Criar uma conta
>> - [x] Criar um usuário
>> - [x] Autenticação do usuário
## Home Page
>> - [x] Mostrar as categorias
>> - [x] Mostrar as subcategorias
>> - [ ] Mostrar os cartões mais bem avaliados
## Search Page
>> - [x] Pesquisar por outros cartões
>> - [x] Ver cartões de negócios de outras empresas e pessoas
## Shared Page
>> - [ ] Fazer pesquisa por QRCode ou NFC
## Profile Page
>> - [ ] Trocar de senha
>> - [ ] Excluir usuário
>> - [ ] Ajustar configuração de distância
>> - [ ] Limpar histórico
## Card Page
>> - [ ] Mostrar o QRCode da url de seu cartão
>> - [ ] Avaliar os cartões
>> - [ ] Adicionar comentários
>> - [ ] Denunciar cartão
>> - [ ] Favoritar os cartões
## Dashboard Page - **Only Web**
>> - [x] Criar seu proprio cartão
>> - [x] Atualizar suas informações no seu cartão
>> - [x] Adicionar informações no seu proprio cartão 
## Dashboard Admin Page - **Only Web**
>> - [x] Adicionar novas categorias
>> - [x] Adicionar novas subcategorias
>> - [ ] Adicionar as subcategorias na(s) categoria(s) especificas

<br>

---

<br>

# Endpoints <br>

## Conta
### POST /api/v1/createAccount
Esse endpoint é responsavel de criar primeiro um usuário e logo em seguida uma conta pro usuário.

#### Parametros
email: O email de cadastro.
password: A senha da conta.
name: O nome do usuário.
nickname: O nome de identificação.
Exemplo do json que deve ser enviado:
```json
{
    "email": "sidneisonic@hotmail.com.br",
    "password": "1234",
    "name": "Sidnei de Souza Junior",
    "nickname": "sanpeta"
}
```

#### Respostas
##### OK! 201
> Caso os dados encaminhados estiverem conforme solicitado o retorno tem de ser do tipo.
Exemplo de respota:
```json
{
    "resposta": "Cadastro realizado com sucesso"
}
```

##### Falha no cadastramento! 202
> Caso essa resposta aconteça, isso signifca que o nickname ou o email já estão sendo utilizados.
Motivos: Email ou Nickname já sendo utilizado.
Exemplo de respota:
```json
{
    "result": "Email ou nickname já está sendo utilizado"
}
```

<br>

---

<br>

### POST /api/v1/auth
Esse endpoint é responsavel por autenticar o usuário.

#### Parametros
email: O email de cadastro.
password: A senha da conta.
Exemplo do json que deve ser enviado:
```json
{
    "email": "sidneisonic@hotmail.com.br",
    "password": "1234"
}
```

#### Respostas
##### OK! 201
> Caso os dados encaminhados estiverem conforme solicitado o retorno tem de ser do tipo. 
Exemplo de respota:
```json
{
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJhZG1pbiI6ZmFsc2UsImVtYWlsIjoic2lkbmVpc29uaWNAaG90bWFpbC5jb20iLCJpYXQiOjE2NDMyMTgxNzUsImV4cCI6MTY0MzM5MDk3NX0.4ajdQRdX4lpKiUYWv6mWNRTsvKBrQYQJURbFhq4BfQ0"
}
```
Se caso a conta criado for admin, esse token expira a cada 10 minutos, enquanto os usuário normais expiram em 2 dias.

##### Falha na autenticação! 401
> Caso essa resposta aconteça, isso signifca que o email e/ou a senha não estão corretos ou até mesmo a conta pode nem ter sido criada.
Motivos: Email ou Senha errado ou conta inexistente.
Exemplo de respota:
```json
{
    "err": "Credencial não autorizada"
}
```

##### Sessão expirada! 400
> Caso essa resposta aconteça, o token expirou.
```json
{
    "err": "Falha interna"
}
```

<br>

---

<br>

## Usuário
### GET /api/v1/users
Esse endpoint é responsavel de buscar todos os usuarios no BD

#### Parametros
Nenhum

#### Respostas
##### OK! 200
> Caso essa rota aconteça voce vai receber a listagem de todos os usuarios
Exemplo de respota:
```json
{
  "name": "Sidnei",
  "table_view_description_content": {
    "items": []
  },
  "table_view_extra_content": {
    "items": []
  },
  "_id": "61ecc7d78de325c5e420fbee",
  "historic": [],
  "tags": [],
"__v": 0
},
...
```

##### Falha na autenticação! 403
> Caso essa resposta aconteça, isso signifca que aconteceu alguma falha durante o processo de autenticacao da requisição.
Motivos: Token inválido, Token expirado, Sem Permissão.
Exemplo de respota:
```json
{
    "success": false,
    "message": "403 - Token Inválido"
}
```
Ou de sem prermissão: 
```json
{
    "success": false,
    "message": "401 - Sem Permissão"
}
```

<br>

---

<br>

### GET /api/v1/user/:nickname
Esse endpoint é responsavel de buscar pelo nickname que for colocado no endpoint

#### Parametros
nickname: é um dos campo que tem de ser único e que facilita na busca 

#### Respostas
##### OK! 200
> Caso essa rota aconteça voce vai receber a informações daquele usuário
Exemplo de respota:
```json
{
    "result": {
        "table_view_description_content": {
            "items": []
        },
        "table_view_extra_content": {
            "items": []
        },
        "_id": "61f17bf1076b396607661f50",
        "email": "sidneisonic@hotmail.com.br",
        "name": "Sidnei de Souza Junior",
        "nickname": "sanpeta",
        "historic": [],
        "tags": [],
        "__v": 0
    }
}
```

##### Usuário não encontrado! 200
> Caso essa resposta aconteça, é porque não tem nenhum usuário com aquele nickname
Motivos: Usuario não encontrado ou Problema interno.
Exemplo de resposta:
```json
{
    result: "Usuario não encontrado"
}
```

<br>

---

<br>

### GET /api/v1/user?nickname=**sanpeta**
Esse endpoint é responsavel de buscar pelo nickname que for colocado no endpoint pelo método query

#### Parametros
nickname: é um dos campo que tem de ser único e que facilita na busca 

#### Respostas
##### OK! 200
> Caso essa rota aconteça voce vai receber a informações daquele usuário
Exemplo de respota:
```json
{
    "result": {
        "table_view_description_content": {
            "items": []
        },
        "table_view_extra_content": {
            "items": []
        },
        "_id": "61f17bf1076b396607661f50",
        "email": "sidneisonic@hotmail.com.br",
        "name": "Sidnei de Souza Junior",
        "nickname": "sanpeta",
        "historic": [],
        "tags": [],
        "__v": 0
    }
}
```

##### Usuário não encontrado! 200
> Caso essa resposta aconteça, é porque não tem nenhum usuário com aquele nickname
Motivos: Usuario não encontrado ou Problema interno.
Exemplo de resposta:
```json
{
  result "Usuario não encontrado"
}
```

<br>

---

<br>

### POST /api/v1/user/card
Esse endpoint é responsavel de buscar pelo email do usuário e modificar as informações do cartão, a origem da requisição tem de possuir autenticação e se é o do mesmo email no qual está querendo ser alterado

#### Parametros
**email**: é o paramentro que deve ser passo pelo body da requisição para fazer a busca
user: é um objeto que possui varios campos e que deve ser olhado o modelo delee também deve ser passado pelo body


#### Respostas
##### OK! 200
> Caso essa tenha feito sucesso em salvar alterações do usuário, ele vai retorna um json de confimação
Exemplo de respota:
```json
{
    result: "Usuário alterado com sucesso"
}
```

##### Usuário não encontrado! 200
> Caso essa resposta aconteça, é porque não tem nenhum usuário com aquele email
Motivos: Usuario não encontrado ou Problema interno.
Exemplo de resposta:
```json
{
    result: "Usuário não encontrado"
}
```

<br>

---

<br>

### POST /api/v1/user/card
Esse endpoint é responsavel de buscar pelo email do usuário e modificar as informações do cartão, a origem da requisição tem de possuir autenticação e se é o do mesmo email no qual está querendo ser alterado

#### Parametros
**email**: é o paramentro que deve ser passo pelo body da requisição para fazer a busca
user: é um objeto que possui varios campos e que deve ser olhado o modelo delee também deve ser passado pelo body


#### Respostas
##### OK! 200
> Caso essa tenha feito sucesso em salvar alterações do usuário, ele vai retorna um json de confimação
Exemplo de respota:
```json
{
    result: "Usuário alterado com sucesso"
}
```

##### Usuário não encontrado! 200
> Caso essa resposta aconteça, é porque não tem nenhum usuário com aquele email
Motivos: Usuario não encontrado ou Problema interno.
Exemplo de resposta:
```json
{
    result: "Usuário não encontrado"
}
```
