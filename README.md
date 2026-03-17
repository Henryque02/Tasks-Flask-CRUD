# 📝 Tasks Flask CRUD

API REST para gerenciamento de tarefas, desenvolvida com Flask. Permite criar, listar, atualizar e deletar tarefas via requisições HTTP.

---

## 🚀 Tecnologias

- **Python** 3.12+
- **Flask** 3.1.3 — framework web
- **Werkzeug** 3.1.6 — utilitários WSGI
- **pytest** 7.4.3 — testes automatizados
- **requests** 2.31.0 — requisições HTTP (usado nos testes)
- **uv** — gerenciador de pacotes e ambientes virtuais

---

## ⚙️ Instalação e uso

### 1. Clone o repositório

```bash
git clone https://github.com/Henryque02/Tasks-Flask-CRUD.git
cd Tasks-Flask-CRUD
```

### 2. Instale as dependências

Com `uv`:

```bash
uv sync
```

Ou com `pip` em um ambiente virtual:

```bash
python -m venv .venv
source .venv/bin/activate  # Linux/macOS
.venv\Scripts\activate     # Windows

pip install -e .
```

### 3. Execute a aplicação

```bash
python app.py
```

A API estará disponível em `http://127.0.0.1:5000`.

### 4. Execute os testes

```bash
pytest tests.py
```

---

## 📄 Documentação da API

O arquivo `assets/openapi.yaml` contém a especificação completa da API no formato **OpenAPI 3.0**, compatível com Swagger UI e Postman.

### Visualizar com Swagger UI

Acesse [editor.swagger.io](https://editor.swagger.io), clique em **File → Import file** e selecione `assets/openapi.yaml`.

### Importar no Postman

Abra o Postman → **Import** → selecione `assets/openapi.yaml`. As rotas serão importadas automaticamente como uma coleção.

---

## 🔌 Endpoints

| Método | Rota | Descrição |
|--------|------|-----------|
| `POST` | `/tasks` | Cria uma nova tarefa |
| `GET` | `/tasks` | Lista todas as tarefas |
| `GET` | `/tasks/<id>` | Retorna uma tarefa pelo ID |
| `PUT` | `/tasks/<id>` | Atualiza uma tarefa pelo ID |
| `DELETE` | `/tasks/<id>` | Remove uma tarefa pelo ID |

## 📁 Estrutura de pastas

```
Tasks-Flask-CRUD/
│
├── models/
│   └── task.py          # Modelo da entidade Task
│
├── assets/
│   └── openapi.yaml     # Especificação OpenAPI 3.0 (Swagger)
│
├── app.py               # Aplicação principal com as rotas
├── tests.py             # Testes automatizados com pytest
├── pyproject.toml       # Configuração do projeto e dependências
├── uv.lock              # Lockfile do uv
├── .python-version      # Versão do Python utilizada
└── .gitignore
```

---

## 👤 Autor

**Henryque** — [@Henryque02](https://github.com/Henryque02)
