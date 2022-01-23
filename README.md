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

src
│   app.js          # Classe app
│   server.js       # Server para iniciar o app
└───api             
  └───controllers   # Funções da controllers do express route
  └───models        # Modelos do banco de dados
  └───services      # Regras de negócio
  └───subscribers   # Eventos async 
  └───repositories* # Query builders 
└───config          # Configuração das variaveis de ambiente
└───jobs            # Tarefas de rotinas
└───loaders         # Modulos para utilizado no app
└───utils           # Trechos de código pequeno
└───helpers         # Trechos de arquitetura de código
└───routes          # Definição de rotas express
└───types           # Tipagem (d.ts) para Typescript

# API Aster Cards

Esta API é utilizada para ...
## Endpoints
### GET /users
Esse endpoint é responsavel de buscar todos os usuarios no BD
#### Parametros
Nenhum
#### Respostas
##### OK! 200
Caso essa rota aconteça voce vai receber a listagem de todos os usuarios
##### Falha na autenticação! 401
> Caso essa resposta aconteça, isso signifca que aconteceu alguma falha durante o processo de autenticacao da requisição.
Motivos: Token inválido, Token expirado.
