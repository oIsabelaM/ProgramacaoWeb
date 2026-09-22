# Aula 08 — Atividade com Projetos Back-end

> Prof. Me. Deivison S. Takatu

> Os trechos marcados como **Complemento** foram acrescentados às anotações (exemplos de código e explicações) e **não estão nos slides**.

## Sumário

1. [Recapitulação: Frameworks e HTTP](#1-recapitulação-frameworks-e-http)
2. [Render para simular Web Services](#2-render-para-simular-web-services)
3. [Evoluindo o projeto Express: CRUD de notas](#3-evoluindo-o-projeto-express-crud-de-notas)
4. [Criando a API REST com CRUD](#4-criando-a-api-rest-com-crud)
5. [Publicando back-end e front-end](#5-publicando-back-end-e-front-end)
6. [Atividade](#6-atividade)
7. [Documentando uma API: Postman](#7-documentando-uma-api-postman)
8. [Referências](#referências)

---

## 1. Recapitulação: Frameworks e HTTP

### Características dos frameworks back-end

- **Estrutura de código organizada:** padrões como MVC, separando lógica de negócio, acesso a dados e rotas
- **Componentização (módulos/serviços):** divisão em módulos independentes, facilitando reuso e atualizações pontuais

### Protocolo HTTP

HTTP é o protocolo que permite a comunicação na web, com as regras de troca de informação entre cliente e servidor.

- **Modelo cliente-servidor:** o navegador (cliente) faz requisições a servidores web
- **Stateless:** cada requisição é independente
- **Baseado em texto:** mensagens legíveis por humanos

### Métodos HTTP

| Método | Finalidade | Características |
|---|---|---|
| **GET** | Recuperar informações | Seguro, idempotente |
| **POST** | Criar novos recursos | Não idempotente |
| **PUT** | Substituir totalmente um recurso | Atualiza informações |
| **PATCH** | Atualizar parcialmente um recurso | Atualiza informações |
| **DELETE** | Remover um recurso | Idempotente |

### JSON

Formato leve de troca de dados, fácil de ler e de gerar por máquinas, baseado em **objetos** (pares nome/valor) e **arrays** (listas ordenadas).

> Este bloco retoma o conteúdo da Aula 07 — ver [aula-07-frameworks-back-end.md](aula-07-frameworks-back-end.md) para a explicação completa.

---

## 2. Render para simular Web Services

Plataforma de hospedagem em nuvem: suporta Node.js, Python e outras linguagens; integração fácil com Git; *deploy* contínuo automático; plano gratuito; interface simples; escalável; SSL grátis; ideal para APIs e microsserviços.

**Benefícios:** *deploy* rápido, configuração sem terminal, atualizações automáticas via GitHub, ambiente de produção profissional, escalabilidade automática, monitoramento integrado, suporte técnico, infraestrutura confiável, ideal para projetos acadêmicos.

### Publicando no Render

1. **Commit do projeto no GitHub:** deixar disponível em um repositório
2. **Criar conta no Render:** acessar `dashboard.render.com`
3. **Criar novo "Web Service":** clicar em *New* e conectar o repositório
4. **Definir comando de start:** *Build Command*: `node`; *Start Command*: `node api.js`
5. **Deploy:** usar a URL gerada, no formato `seu-projeto.onrender.com`

---

## 3. Evoluindo o projeto Express: CRUD de notas

Depois de recapitular o que foi feito na aula anterior (uma rota simples de data e hora), o projeto evolui: em vez de exibir a data de forma estática, a aplicação passa a **armazenar, visualizar, editar e excluir notas**, aplicando na prática o **CRUD** (*Create, Read, Update, Delete*).

**Estrutura do projeto:**

| Arquivo | Função |
|---|---|
| `data.json` | Armazena as notas criadas pelo usuário |
| `server.js` | Configura e executa o servidor Express, expondo a API RESTful de CRUD |

**Complemento — o que é CRUD, em uma frase por operação:**

| Letra | Operação | Verbo HTTP típico |
|---|---|---|
| **C**reate | Criar um novo registro | `POST` |
| **R**ead | Ler um ou mais registros | `GET` |
| **U**pdate | Atualizar um registro existente | `PUT` / `PATCH` |
| **D**elete | Remover um registro | `DELETE` |

### Rotas CRUD da aplicação

| Rota | Descrição |
|---|---|
| `GET /api/notes` | Lista todas as notas armazenadas |
| `POST /api/notes` | Adiciona uma nova nota (exige `titulo` e `texto`; recebe um ID único via `Date.now().toString()` e a data de criação) |
| `PUT /api/notes/:id` | Atualiza uma nota existente pelo ID (exige `titulo` e `texto`) |
| `DELETE /api/notes/:id` | Remove uma nota pelo ID (retorna status `204` se a exclusão for bem-sucedida) |

---

## 4. Criando a API REST com CRUD

**Passo 1 — Criar a pasta do projeto:** `projeto-notas`, aberta no VS Code.

**Passo 2 — Instalar o Express:**

```bash
npm install express
```

**Passo 3 — Instalar o Body-Parser:**

```bash
npm install body-parser
```

> O **Body-Parser** é a biblioteca que permite ao servidor ler dados enviados no corpo das requisições HTTP, como JSON em métodos `POST` e `PUT`.

**Passo 4 — Criar o arquivo principal `server.js`**, seguindo os trechos abaixo.

### Configuração inicial

```javascript
// Importa o Express, Body-Parser e FS
const express = require('express');
const bodyParser = require('body-parser');
const fs = require('fs');
const app = express();
const PORT = 3000;
const FILE = 'data.json';

// Permite receber JSON
app.use(bodyParser.json());

// Libera acesso externo (CORS)
app.use((req, res, next) => {
  res.header('Access-Control-Allow-Origin', '*');
  next();
});
```

### Funções auxiliares e rota GET

```javascript
// Função para ler arquivo
function readNotes() {
  try {
    const data = fs.readFileSync(FILE);
    return JSON.parse(data);
  } catch {
    return [];
  }
}

// Função para salvar arquivo
function saveNotes(notes) {
  fs.writeFileSync(FILE, JSON.stringify(notes, null, 2));
}

// GET - Listar notas
app.get('/api/notes', (req, res) => {
  const notes = readNotes();
  res.json(notes);
});
```

**Complemento:** `readNotes` usa `try/catch` porque, se o arquivo `data.json` ainda não existir (primeira execução), `fs.readFileSync` lança um erro — nesse caso, a função devolve uma lista vazia em vez de travar o servidor.

### POST — Criar nota

```javascript
app.post('/api/notes', (req, res) => {
  const notes = readNotes();

  const novaNota = {
    id: Date.now().toString(),
    titulo: req.body.titulo,
    texto: req.body.texto
  };

  notes.push(novaNota);
  saveNotes(notes);

  res.json(novaNota);
});
```

### PUT — Editar nota

```javascript
app.put('/api/notes/:id', (req, res) => {
  const notes = readNotes();

  const index = notes.findIndex(n => n.id === req.params.id);

  if (index >= 0) {
    notes[index].titulo = req.body.titulo;
    notes[index].texto = req.body.texto;
    saveNotes(notes);
    res.json(notes[index]);
  } else {
    res.status(404).json({ erro: 'Nota não encontrada' });
  }
});
```

### DELETE — Excluir nota e iniciar o servidor

```javascript
app.delete('/api/notes/:id', (req, res) => {
  const notes = readNotes();

  const novasNotas = notes.filter(n => n.id !== req.params.id);

  saveNotes(novasNotas);

  res.json({ mensagem: 'Nota removida' });
});

// Inicia servidor
app.listen(PORT, () => {
  console.log('Servidor rodando em http://localhost:3000');
});
```

**Complemento — por que `:id` na rota?** Os dois-pontos marcam um **parâmetro de rota**. Em `/api/notes/:id`, o trecho depois da última barra vira `req.params.id` dentro da função — por exemplo, uma requisição para `/api/notes/123` chega com `req.params.id` igual a `"123"`.

### Passo 5 — Arquivo de dados

Criar um arquivo `data.json`:

```json
[
  {
    "id": "1",
    "titulo": "Lembretes",
    "texto": "Comprar leite e pão",
    "criadoEm": "2025-04-29T10:00:00Z"
  },
  {
    "id": "2",
    "titulo": "Tarefas do trabalho",
    "texto": "Enviar relatório até sexta-feira",
    "criadoEm": "2025-04-29T10:00:00Z"
  }
]
```

### Passo 6 — Executar o servidor

```bash
node server.js
```

---

## 5. Publicando back-end e front-end

**Passo 7 — Criar o front-end em React:** interface para listar, cadastrar, editar e excluir notas, consumindo a API.

**Passo 8 — Publicar o back-end no Render:** enviar o projeto Express para o GitHub e fazer o *deploy* no Render.

**Passo 9 — Conectar a API no React:** copiar a URL gerada no Render e substituir `http://localhost:3000/api/notes` no React pelo *endpoint* online.

**Passo 10 — Publicar o front-end na Vercel:** enviar o projeto React para o GitHub e fazer o *deploy* na Vercel.

**Complemento — exemplo de chamada da API a partir do React** (usando `fetch`, depois de trocar a URL local pela do Render):

```jsx
const API_URL = 'https://seu-projeto.onrender.com/api/notes';

// Listar notas
fetch(API_URL)
  .then((res) => res.json())
  .then((notas) => console.log(notas));

// Criar nota
fetch(API_URL, {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  body: JSON.stringify({ titulo: 'Nova nota', texto: 'Conteúdo da nota' }),
});
```

---

## 6. Atividade

1. Após desenvolver a aplicação com Express.js, fazer o *deploy* do back-end no Render, garantindo que a API fique acessível online.
2. Construir uma aplicação front-end que consuma as rotas criadas, permitindo ao usuário realizar todas as operações **CRUD** (criar, visualizar, editar e excluir notas), interagindo diretamente com o arquivo JSON usado no back-end.
3. Organizar tudo em um documento com prints do código, da aplicação em funcionamento, o link do repositório no GitHub e o link do *deploy* na Vercel.

**Referência de projetos-exemplo do professor:**

- <https://github.com/deivisontakatu/exemplo-api-backend>
- <https://github.com/deivisontakatu/exemplo-api-frontend>

### Questões para refletir

- Quais são os riscos de segurança desse projeto e como poderiam ser eliminados ou mitigados?
- Usar um arquivo JSON (`data.json`) para armazenar notas é uma boa prática em produção? Quais são as vantagens e desvantagens dessa abordagem?
- Quais limitações um servidor baseado em arquivo JSON teria se o número de notas crescesse para 10.000 registros?
- O código atual está todo em `server.js`. Por que isso é problemático e como você melhoraria a organização da lógica?

---

## 7. Documentando uma API: Postman

Normalmente, as APIs são acompanhadas de uma **documentação técnica** que descreve em detalhes como utilizá-las: os *endpoints* disponíveis, os métodos HTTP suportados, os parâmetros exigidos, os formatos de resposta e exemplos de requisições.

### Postman

Ferramenta colaborativa de desenvolvimento de APIs, que simplifica criar, testar, documentar e monitorar requisições HTTP.

- Interface intuitiva para enviar solicitações (`GET`, `POST`, `PUT`, `DELETE` etc.)
- Analisa respostas e automatiza testes, sem precisar de linha de comando ou código complexo
- Essencial para desenvolvedores, engenheiros de QA e equipes de DevOps

**Recursos:**

- **Coleções de requisições:** organização e compartilhamento de *endpoints* entre equipes
- **Variáveis de ambiente, scripts pré-*request* e testes automatizados:** garantem confiabilidade e eficiência
- **Documentação automática** e integração com pipelines de CI/CD via **Newman** (CLI do Postman)
- **Mock Servers:** simulam APIs antes da implementação
- **Monitoramento:** verifica a disponibilidade dos *endpoints*
- Suporte a **GraphQL**, **WebSockets** e autenticação **OAuth 2.0**

A versão gratuita já é poderosa; planos empresariais incluem colaboração em tempo real e gerenciamento de APIs em larga escala. Fonte: [postman.com](https://www.postman.com/).

**Complemento — passo a passo básico para documentar o CRUD de notas no Postman:**

1. Criar uma **coleção** nova (ex.: "API de Notas")
2. Adicionar uma requisição para cada rota: `GET /api/notes`, `POST /api/notes`, `PUT /api/notes/:id`, `DELETE /api/notes/:id`
3. Em cada requisição `POST`/`PUT`, na aba *Body*, escolher `raw` → `JSON` e escrever o exemplo de corpo (`{ "titulo": "...", "texto": "..." }`)
4. Adicionar uma descrição em cada requisição, explicando o que ela faz e os possíveis códigos de resposta (`200`, `201`, `204`, `404`)
5. Salvar e, se quiser, clicar em **Share** para gerar o link da coleção

### Atividade (continuação)

4. Criar uma coleção no Postman documentando as quatro operações CRUD da API criada.
5. Configurar as requisições HTTP e definir os parâmetros de cada *endpoint*, com descrições claras sobre os códigos de resposta.
6. Organizar tudo em um documento com prints do código, da aplicação em funcionamento e o link da coleção do Postman. Enviar o documento como entrega da atividade no repositório da disciplina.

---

## Referências

DINIZ, Luciana Mara Freitas et al. Aprendizado Baseado em Projetos em IHC (presencial e remoto): prototipação segundo as heurísticas de Nielsen. In: SIMPÓSIO BRASILEIRO DE FATORES HUMANOS EM SISTEMAS COMPUTACIONAIS (IHC). SBC, 2020. p. 13-18.

GONÇALVES, Rodrigo Franco et al. Uma proposta de processo de produção de aplicações Web. **Production**, v. 15, p. 376-389, 2005.

LUCASSEN, Garm et al. The use and effectiveness of user stories in practice. In: REQUIREMENTS ENGINEERING: FOUNDATION FOR SOFTWARE QUALITY, 22., 2016, Gothenburg. **Proceedings** [...]. Springer International Publishing, 2016. p. 205-222.

SALINAS, C.; SEDEÑO, J.; CUARESMA, M.; RISOTO, M. Agile, Web Engineering and Capability Maturity Model Integration: A systematic literature review. **Information and Software Technology**, v. 71, p. 92-107, 2016. DOI: 10.1016/J.INFSOF.2015.11.002.

NGUYEN, Hong-Thu Thi. Website Builder as an Assistive Technology Tool for Reflection, Collaboration and Skills Development in Learning ESP. **Journal of Learning for Development**, v. 11, n. 1, p. 138-150, 2024.
