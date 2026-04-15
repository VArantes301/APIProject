# 📋 API de Gerenciamento de Tarefas

API REST para criação e gerenciamento de tarefas, construída com **Node.js puro**, sem o uso de frameworks externos como Express.

**Autor:** Vincentt Arantes  
**Turma:** 2 DS AMS — Campinas, São Paulo  

---

## 🚀 Tecnologias Utilizadas

- **Node.js** — runtime JavaScript no servidor
- **Módulo `http`** nativo do Node.js (sem frameworks)
- Arquitetura em camadas: **Routes → Controller → Service → Model**

---

## 📁 Estrutura do Projeto

```
APIProject/
├── app.js                          # Ponto de entrada — cria e inicia o servidor HTTP
└── src/
    ├── routes/
    │   └── taskRoutes              # Define e mapeia as rotas da API
    ├── controller/
    │   └── taskController.js       # Recebe as requisições e chama os serviços
    ├── services/
    │   └── taskServices            # Contém a lógica de negócio
    └── model/
        └── taskModel               # Define a estrutura de uma tarefa
```

---

## ⚙️ Como Executar

### Pré-requisitos

- [Node.js](https://nodejs.org/) instalado na máquina

### Passos

1. Clone ou extraia o projeto:
```bash
git clone <url-do-repositorio>
cd APIProject
```

2. Inicie o servidor:
```bash
node app.js
```

3. O servidor estará disponível em:
```
http://localhost:3000
```

> ⚠️ Os dados são armazenados **em memória**. Ao reiniciar o servidor, todas as tarefas serão apagadas.

---

## 🔗 Endpoints

| Método   | Rota                    | Descrição                            |
|----------|-------------------------|--------------------------------------|
| `GET`    | `/tasks`                | Lista todas as tarefas               |
| `GET`    | `/tasks/:id`            | Busca uma tarefa pelo ID             |
| `POST`   | `/tasks`                | Cria uma nova tarefa                 |
| `PUT`    | `/tasks/:id`            | Atualiza o título de uma tarefa      |
| `PUT`    | `/tasks/:id/completed`  | Marca ou desmarca tarefa como concluída |
| `DELETE` | `/tasks/:id`            | Remove uma tarefa                    |

---

## 📨 Exemplos de Uso

### ➕ Criar uma tarefa

**Request:**
```http
POST /tasks
Content-Type: application/json

{
  "title": "Estudar Node.js"
}
```

**Response** `201 Created`:
```json
{
  "id": 1,
  "title": "Estudar Node.js",
  "completed": false
}
```

---

### 📄 Listar todas as tarefas

**Request:**
```http
GET /tasks
```

**Response** `200 OK`:
```json
[
  {
    "id": 1,
    "title": "Estudar Node.js",
    "completed": false
  }
]
```

---

### 🔍 Buscar tarefa por ID

**Request:**
```http
GET /tasks/1
```

**Response** `200 OK`:
```json
{
  "id": 1,
  "title": "Estudar Node.js",
  "completed": false
}
```

**Response** `404 Not Found` (se não existir):
```json
{
  "message": "Tarefa não encontrada"
}
```

---

### ✏️ Atualizar o título de uma tarefa

**Request:**
```http
PUT /tasks/1
Content-Type: application/json

{
  "title": "Estudar Express.js"
}
```

**Response** `200 OK`:
```json
{
  "id": 1,
  "title": "Estudar Express.js",
  "completed": false
}
```

---

### ✅ Marcar tarefa como concluída (ou desfazer)

**Request:**
```http
PUT /tasks/1/completed
Content-Type: application/json

{
  "completed": true
}
```

**Response** `200 OK`:
```json
{
  "id": 1,
  "title": "Estudar Express.js",
  "completed": true
}
```

---

### 🗑️ Deletar uma tarefa

**Request:**
```http
DELETE /tasks/1
```

**Response** `200 OK`:
```json
{
  "message": "Removida"
}
```

**Response** `404 Not Found` (se não existir):
```json
{
  "message": "Não encontrada"
}
```

---

## 🧱 Arquitetura

O projeto segue o padrão de camadas **MVC simplificado**:

```
Requisição HTTP
      │
      ▼
  taskRoutes        → identifica método e rota, extrai parâmetros
      │
      ▼
taskController      → lê o body da requisição, chama o serviço e envia a resposta
      │
      ▼
 taskServices       → executa a lógica de negócio (CRUD em memória)
      │
      ▼
  taskModel         → define a estrutura do objeto tarefa { id, title, completed }
```

---

## 📌 Observações

- A API **não utiliza banco de dados** — os dados ficam armazenados em um array em memória (`tasks[]`).
- Os IDs são gerados automaticamente por um contador incremental (`idCounter`).
- Toda comunicação é feita em **JSON**.
- O servidor roda na porta **3000** por padrão.
