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
>> - [ ] Criar sua conta
>> - [ ] Autenticação em sua conta 
>> - [ ] Ver cartões de negócios de outras empresas e pessoas
>> - [ ] Criar seu proprio cartão 
>> - [ ] Adicionar informações no seu proprio cartão
>> - [ ] Atualizar suas informações no seu cartão
>> - [ ] Adicionar novas categorias e subcategorias, mostrar os cartões mais bem avaliados
>> - [ ] Favoritar seus cartões favoritos, buscar informações
>> - [ ] Pesquisar por outros cartões
>> - [ ] Trocar de senha
>> - [ ] Excluir conta
>> - [ ] Ajustar configuração de distância
>> - [ ] Limpar histórico
>> - [ ] Mostrar seu QRCode
>> - [ ] Fazer pesquisa por QRCode ou NFC
>> - [ ] Avaliar os cartões
>> - [ ] Adicionar comentários
>> - [ ] Denunciar cartão

## Endpoints
### **GET /users**
Esse endpoint é responsavel de buscar todos os usuarios no BD

#### Parametros
Nenhum

#### Respostas
##### OK! 200
> Caso essa rota aconteça voce vai receber a listagem de todos os usuarios
Exemplo de respota:
```
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
}
```

##### Falha na autenticação! 401
> Caso essa resposta aconteça, isso signifca que aconteceu alguma falha durante o processo de autenticacao da requisição.
Motivos: Token inválido, Token expirado.
