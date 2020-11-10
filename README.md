
<img alt="GoStack" src="https://storage.googleapis.com/golden-wind/bootcamp-gostack/header-desafios-new.png" />

<h3 align="center">
  Desafio 06: Banco de dados e upload de arquivos no Node.js
</h3>

## :rocket: Sobre o desafio

Esse projeto consiste em uma aplicação Node incluindo banco de dados e envio de arquivos com o Multer. Nele são armazenadas transações financeiras de entrada e saída, permitindo o cadastro e listagem dessas transações, além de permitir a criação de novos registros no banco de dados a partir do envio de um arquivo csv.

## :motorway: Rotas da aplicação

- **`POST /transactions`**: A rota recebe `title`, `value`, `type`, e `category` dentro do corpo da requisição, sendo o `type` o tipo da transação, que deve ser `income` para entradas (depósitos) e `outcome` para saídas (retiradas). Ao cadastrar uma nova transação, ela é armazenada dentro do seu banco de dados, possuindo os campos `id`, `title`, `value`, `type`, `category_id`, `created_at`, `updated_at`.

```json
{
  "id": "uuid",
  "title": "Salário",
  "value": 3000,
  "type": "income",
  "category": "Alimentação"
}
```

- **`GET /transactions`**: Essa rota retorna uma listagem com todas as transações que você cadastrou até agora, junto com o valor da soma de entradas, retiradas e total de crédito. O objeto de retorno possui o seguinte formato:

```json
{
  "transactions": [
    {
      "id": "uuid",
      "title": "Salário",
      "value": 4000,
      "type": "income",
      "category": {
        "id": "uuid",
        "title": "Salary",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    },
    {
      "id": "uuid",
      "title": "Freela",
      "value": 2000,
      "type": "income",
      "category": {
        "id": "uuid",
        "title": "Others",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    },
    {
      "id": "uuid",
      "title": "Pagamento da fatura",
      "value": 4000,
      "type": "outcome",
      "category": {
        "id": "uuid",
        "title": "Others",
        "created_at": "2020-04-20T00:00:49.620Z",
        "updated_at": "2020-04-20T00:00:49.620Z"
      },
      "created_at": "2020-04-20T00:00:49.620Z",
      "updated_at": "2020-04-20T00:00:49.620Z"
    }
  ],
  "balance": {
    "income": 6000,
    "outcome": 4000,
    "total": 2000
  }
}
```

- **`DELETE /transactions/:id`**: A rota deleta uma transação com o `id` presente nos parâmetros da rota;

* **`POST /transactions/import`**: A rota permite a importação de um arquivo com formato `.csv` contendo as mesmas informações necessárias para criação de uma transação `id`, `title`, `value`, `type`, `category_id`, `created_at`, `updated_at`, onde cada linha do arquivo CSV deve ser um novo registro para o banco de dados, e por fim retorne todas as `transactions` que foram importadas para seu banco de dados. 


## :computer: Instruções de instalação e teste
Clone o repositório usando o `git` ou faça o download no formato zip. 
Antes de tudo, certifique-se de que você tem um gerenciador de pacotes (como o yarn), o `Node.js` e o Docker (com a imagem PostgreSQL) instalados em sua máquina.

Com o Docker rodando, entre no seu gerenciador de banco de dados de preferência e crie 2 databases:

- **`gostack_desafio06`**
- **`gostack_desafio06_tests`**

Após baixar o projeto, abra uma aba do terminal e execute os seguintes comandos:

```Bash
# ../pasta-de-destino
$ cd gostack-typeorm-upload
# ../pasta-de-destino/gostack-typeorm-upload
$ yarn
```

Para rodar as migrations e criar as tabelas no banco de dados:

```Bash
# ../pasta-de-destino/gostack-typeorm-upload
$ yarn typeorm migration:run
```

Para iniciar a aplicação na porta 3333:

```Bash
# ../pasta-de-destino/gostack-typeorm-upload
$ yarn dev:server
```

Para rodar os testes da aplicação (utilizando a database gostack_desafio06_tests criada anteriormente):
```Bash
# ../pasta-de-destino/gostack-typeorm-upload
$ yarn test
```
