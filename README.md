# API de Tarefas

API REST para gerenciamento de tarefas, construída com Node.js puro (sem frameworks).

**Autor:** Vincentt Arantes  
**Turma:** 2 DS AMS — Bento Quirino, Campinas/SP

---

## Como rodar

```bash
node app.js
```

Servidor disponível em `http://localhost:3000`

---

## Endpoints

| Método | Rota | Descrição |
|--------|------|-----------|
| `GET` | `/tasks` | Lista todas as tarefas |
| `POST` | `/tasks` | Cria uma nova tarefa |
| `PUT` | `/tasks/:id` | Atualiza o título de uma tarefa |
| `PUT` | `/tasks/:id/completed` | Marca/desmarca como concluída |
| `DELETE` | `/tasks/:id` | Remove uma tarefa |

---

## Exemplos

**Criar tarefa**
```http
POST /tasks
Content-Type: application/json

{ "title": "Estudar Node.js" }
```

**Atualizar título**
```http
PUT /tasks/1
Content-Type: application/json

{ "title": "Novo título" }
```

**Concluir tarefa**
```http
PUT /tasks/1/completed
Content-Type: application/json

{ "completed": true }
```

**Deletar tarefa**
```http
DELETE /tasks/1
```

---

## Estrutura

```
API/
├── app.js
└── src/
    ├── controller/taskController
    ├── model/taskModel
    ├── routes/taskRoutes
    └── services/taskServices
```

> Os dados são armazenados em memória — reiniciar o servidor apaga as tarefas.
