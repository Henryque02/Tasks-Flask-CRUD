# Tasks Flask CRUD

Uma API REST simples para gerenciamento de tarefas, construída com Python e Flask. Este projeto demonstra os fundamentos das operações CRUD (Create, Read, Update, Delete) utilizando armazenamento em memória.

## Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [Como Começar](#como-começar)
  - [Pré-requisitos](#pré-requisitos)
  - [Instalação](#instalação)
  - [Executando o Servidor](#executando-o-servidor)
- [Endpoints da API](#endpoints-da-api)
  - [Criar uma Tarefa](#criar-uma-tarefa)
  - [Listar Todas as Tarefas](#listar-todas-as-tarefas)
  - [Buscar Tarefa por ID](#buscar-tarefa-por-id)
  - [Atualizar uma Tarefa](#atualizar-uma-tarefa)
  - [Deletar uma Tarefa](#deletar-uma-tarefa)
- [Executando os Testes](#executando-os-testes)

---

## Sobre o Projeto

Esta API permite gerenciar uma lista de tarefas. Cada tarefa possui um título, uma descrição opcional e um status de conclusão. Todos os dados são armazenados em memória, ou seja, são redefinidos toda vez que o servidor é reiniciado. O projeto é voltado para aprendizado de desenvolvimento de APIs REST com Flask.

## Tecnologias Utilizadas

| Ferramenta | Versão | Finalidade |
|------------|--------|------------|
| Python | 3.12+ | Linguagem de programação |
| Flask | ≥ 3.1.3 | Framework web |
| Werkzeug | ≥ 3.1.6 | Utilitários WSGI (dependência do Flask) |
| pytest | 7.4.3 | Framework de testes |
| requests | 2.31.0 | Cliente HTTP utilizado nos testes |
| uv | — | Gerenciador de pacotes Python moderno |

## Estrutura do Projeto

```
Tasks-Flask-CRUD/
├── app.py                    # Aplicação Flask e definição das rotas
├── models/
│   └── task.py              # Classe do modelo de Tarefa
├── tests.py                 # Testes de integração
├── pyproject.toml           # Metadados e dependências do projeto
├── uv.lock                  # Versões fixadas das dependências
├── assets/
│   ├── documentation.x-yaml # Especificação OpenAPI 3.0
│   └── postman.x-yaml       # Coleção do Postman
└── README.md
```

## Como Começar

### Pré-requisitos

- Python 3.12 ou superior
- [uv](https://docs.astral.sh/uv/) (recomendado) **ou** pip

### Instalação

**Usando uv (recomendado):**

```bash
uv sync
```

**Usando pip:**

```bash
pip install flask werkzeug
```

### Executando o Servidor

```bash
python app.py
```

O servidor iniciará em modo de depuração e estará disponível em `http://127.0.0.1:5000`.

---

## Endpoints da API

### Criar uma Tarefa

**POST** `/tasks`

Cria uma nova tarefa.

**Corpo da requisição:**

```json
{
  "title": "Comprar mantimentos",
  "description": "Leite, ovos, pão"
}
```

> `description` é opcional.

**Resposta** `200 OK`:

```json
{
  "message": "Nova tarefa criada com sucesso!",
  "id": 1
}
```

---

### Listar Todas as Tarefas

**GET** `/tasks`

Retorna a lista de todas as tarefas.

**Resposta** `200 OK`:

```json
{
  "tasks": [
    {
      "id": 1,
      "title": "Comprar mantimentos",
      "description": "Leite, ovos, pão",
      "completed": false
    }
  ],
  "total_tasks": 1
}
```

---

### Buscar Tarefa por ID

**GET** `/tasks/<id>`

Retorna uma única tarefa pelo seu ID.

**Resposta** `200 OK`:

```json
{
  "id": 1,
  "title": "Comprar mantimentos",
  "description": "Leite, ovos, pão",
  "completed": false
}
```

**Resposta** `404 Not Found`:

```json
{
  "message": "Não foi possível encontrar a atividade"
}
```

---

### Atualizar uma Tarefa

**PUT** `/tasks/<id>`

Atualiza o título, a descrição e o status de conclusão de uma tarefa.

**Corpo da requisição:**

```json
{
  "title": "Comprar mantimentos",
  "description": "Leite, ovos, pão, manteiga",
  "completed": true
}
```

**Resposta** `200 OK`:

```json
{
  "message": "Tarefa atualizada com sucesso"
}
```

**Resposta** `404 Not Found`:

```json
{
  "message": "Não foi possível encontrar a atividade"
}
```

---

### Deletar uma Tarefa

**DELETE** `/tasks/<id>`

Deleta uma tarefa pelo seu ID.

**Resposta** `200 OK`:

```json
{
  "message": "Tarefa deletada com sucesso"
}
```

**Resposta** `404 Not Found`:

```json
{
  "message": "Não foi possível encontrar a atividade"
}
```

---

## Executando os Testes

A suíte de testes utiliza `pytest` e faz requisições HTTP reais, portanto **o servidor Flask precisa estar em execução** antes de rodar os testes.

1. Inicie o servidor em um terminal:

```bash
python app.py
```

2. Em outro terminal, execute os testes:

```bash
pytest tests.py -v
```