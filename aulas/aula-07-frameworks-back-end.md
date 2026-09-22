# Aula 07 — Introdução a Frameworks Back-end

> Prof. Me. Deivison S. Takatu

> Os trechos marcados como **Complemento** foram acrescentados às anotações (exemplos de código e explicações) e **não estão nos slides**.

## Sumário

1. [Frameworks back-end](#1-frameworks-back-end)
2. [Arquitetura e Design Patterns](#2-arquitetura-e-design-patterns)
3. [Framework Express.js](#3-framework-expressjs)
4. [Introdução às APIs](#4-introdução-às-apis)
5. [Criando uma API REST com Express](#5-criando-uma-api-rest-com-express)
6. [Atividade](#6-atividade)
7. [Referências](#referências)

---

## 1. Frameworks back-end

Conjunto de **ferramentas, bibliotecas e convenções** que padroniza o desenvolvimento da lógica de servidor, APIs e integrações de banco de dados, facilitando sistemas escaláveis, seguros e de fácil manutenção.

| Sem framework | Com framework |
|---|---|
| Código manual, configurações repetitivas | Rotas organizadas |
| Maior risco de vulnerabilidades | Segurança integrada (autenticação, validações) |
| Dificuldade em escalar | Gerenciamento de banco de dados simplificado, desempenho otimizado |

Referência: Freeman; Robson (2022).

### Características dos frameworks back-end

- **Estrutura de código organizada:** padrões como **MVC** (Modelo, Visão, Controlador) ou arquitetura em camadas, separando lógica de negócio, acesso a dados e rotas
- **Componentização (módulos/serviços):** divisão em módulos independentes (ex.: microsserviços, *middlewares*), facilitando reuso e atualizações pontuais
- **Programação assíncrona:** suporte nativo a operações não bloqueantes (Node.js com Express, Python com `async/await`), melhorando a performance em I/O pesado (banco de dados, APIs externas)
- **Padrões de segurança:** proteção automática contra *SQL injection* e sistemas de *logging* para auditoria
- **Sistema de rotas e APIs:** gerenciamento de *endpoints* RESTful ou GraphQL, com autenticação integrada (JWT, OAuth)

### Exemplos de frameworks

| Framework | Linguagem | Características |
|---|---|---|
| **Express.js** | Node.js | Minimalista e flexível; estendido por *middlewares* (autenticação, validação, roteamento) |
| **Django** | Python | *Full-stack*, segue o padrão MVC; inclui ORM, autenticação e painel administrativo prontos |
| **Laravel** | PHP | Sintaxe elegante, ORM (Eloquent), rotas intuitivas, CLI Artisan para automatizar tarefas |

> A escolha do framework impacta desempenho, escalabilidade, manutenção e experiência do usuário. Considere complexidade do projeto, curva de aprendizado, desempenho e suporte da comunidade. Comparativo: [StackShare](https://stackshare.io/stackups).

---

## 2. Arquitetura e Design Patterns

A **arquitetura de software** e os *design patterns* determinam a escalabilidade, manutenção e desempenho do sistema. Uma decisão bem fundamentada evita retrabalho, reduz custos e garante um sistema adaptável a futuras demandas.

**Fatores de decisão:** requisitos do projeto, complexidade e tamanho da equipe; alinhamento com objetivos de negócio e tecnologia.

Referência: Rockford (2008).

### Design Patterns (padrões de projeto)

| Categoria | Função | Exemplos |
|---|---|---|
| **Criacionais** | Controlam a criação de objetos, com flexibilidade e reuso de código com baixo acoplamento | Factory, Singleton, Builder |
| **Estruturais** | Organizam classes e objetos em estruturas maiores, mantendo eficiência e clareza na arquitetura | Adapter, Composite, Proxy |
| **Comportamentais** | Gerenciam a comunicação entre objetos, distribuindo responsabilidades | Observer, Strategy, Command |

Fonte: [refactoring.guru/design-patterns/catalog](https://refactoring.guru/design-patterns/catalog).

**Complemento — para que servem na prática:**

- **Singleton:** garante que uma classe tenha só **uma instância** em todo o sistema (ex.: uma única conexão com o banco de dados compartilhada pela aplicação).
- **Factory:** centraliza a criação de objetos, para que quem usa não precise saber os detalhes de como construí-los (ex.: uma função que cria diferentes tipos de notificação — e-mail, SMS — a partir de um único ponto).
- **Observer:** um objeto avisa vários outros quando algo muda, sem eles precisarem perguntar o tempo todo (ex.: quando uma nota é criada na API, o front-end é avisado para atualizar a lista).

### Monolito x Microsserviço

| Monolito | Microsserviço |
|---|---|
| Aplicação única, todos os módulos integrados em um único código | Aplicação dividida em serviços independentes |
| Simples de desenvolver | Permite escalabilidade e flexibilidade |
| Difícil de escalar | Maior complexidade operacional |
| Ideal para projetos pequenos | Atende melhor sistemas complexos e em crescimento |

A escolha depende do tamanho, da equipe e das necessidades futuras do projeto. Fonte: [atlassian.com](https://www.atlassian.com/). Referência: Newman (2021).

### Estudo de caso: Amazon Prime Video

Em 2023, a Amazon Prime Video **voltou** de uma arquitetura de microsserviços serverless para uma arquitetura **monolítica**, o que reduziu custos em 90% ao eliminar gargalos de comunicação entre serviços. O caso mostra que escolhas arquiteturais devem considerar as necessidades específicas do projeto, sem seguir tendências cegamente — microsserviços continuam válidos em outros cenários.

**Lição:** arquiteturas distribuídas trazem custos ocultos de coordenação; soluções monolíticas podem ser mais eficientes quando há forte acoplamento entre componentes e baixa necessidade de escalabilidade independente. Fonte: [thenewstack.io](https://thenewstack.io/).

---

## 3. Framework Express.js

O **Express.js** é um framework para Node.js que facilita a criação de servidores web e APIs. É minimalista, flexível e muito popular no ecossistema JavaScript.

- **Simplifica o Node.js:** o Node.js puro (módulo `http`) exige mais código para rotas e *middlewares*; o Express torna isso mais fácil
- **Roteamento:** facilita definir rotas (ex.: `/users`, `/products`)
- **Middlewares:** funções que processam requisições/respostas (ex.: autenticação, logs)
- **Velocidade:** leve e rápido para criar APIs ou servidores web

### Exemplo de código

Quando `http://localhost:3000` é acessado, o Express responde com "Olá, mundo!". `app.get()` define uma rota para o método HTTP GET.

**Complemento — o exemplo por extenso:**

```javascript
const express = require('express');
const app = express();
const PORT = 3000;

app.get('/', (req, res) => {
  res.send('Olá, mundo!');
});

app.listen(PORT, () => {
  console.log(`Servidor rodando em http://localhost:${PORT}`);
});
```

### Node.js puro x Express.js

**Complemento — a mesma rota nos dois estilos:**

```javascript
// Node.js puro (módulo http)
const http = require('http');

const server = http.createServer((req, res) => {
  if (req.url === '/' && req.method === 'GET') {
    res.writeHead(200, { 'Content-Type': 'text/plain' });
    res.end('Olá, mundo!');
  }
});

server.listen(3000);
```

```javascript
// Express.js
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.send('Olá, mundo!');
});

app.listen(3000);
```

O Node.js puro exige checar manualmente a URL e o método a cada rota nova; o Express organiza isso com `app.get()`, `app.post()` etc.

### Quando usar Express.js

1. Para **APIs REST** eficientes, integração com bancos de dados e *backends* escaláveis para aplicações web e mobile
2. Ideal para servir páginas com *templates* e *middlewares* que simplificam autenticação, logs e tratamento de erros
3. **Evitar** para aplicações em tempo real (prefira WebSockets) ou processamento pesado (use *Workers*); é melhor para prototipagem rápida

### Como funciona uma requisição na prática

1. **Navegador / front-end:** o usuário acessa a página ou clica em um botão
2. **Requisição HTTP:** o navegador envia uma requisição ao servidor (`GET`, `POST`, `PUT`, `DELETE`)
3. **Servidor Express.js:** o *backend* recebe a requisição, identifica a rota e executa a lógica necessária
4. **Banco de dados / API externa:** o servidor busca, grava ou atualiza informações
5. **Resposta JSON:** o servidor retorna os dados processados
6. **Atualização da tela:** o front-end recebe a resposta e exibe os dados ao usuário

---

## 4. Introdução às APIs

### Protocolo HTTP

HTTP (*Hypertext Transfer Protocol*) é o protocolo que permite a comunicação na *World Wide Web*, estabelecendo as regras para a troca de informações entre clientes (navegadores) e servidores.

**Conceitos principais:**

- **Modelo cliente-servidor:** o navegador (cliente) faz requisições a servidores web
- **Stateless (sem estado):** cada requisição é independente; o servidor não "lembra" de requisições anteriores
- **Baseado em texto:** as mensagens são legíveis por humanos

### Métodos HTTP

| Método | Finalidade | Características |
|---|---|---|
| **GET** | Recuperar informações do servidor | Seguro (não altera dados); idempotente (várias chamadas = mesmo resultado) |
| **POST** | Criar novos recursos no servidor | Não idempotente (chamadas repetidas criam vários recursos) |
| **PUT** | Substituir completamente um recurso existente | Serve para atualizar informações |
| **PATCH** | Atualizar parcialmente um recurso | Serve para atualizar informações |
| **DELETE** | Remover um recurso específico | Idempotente (apagar algo já apagado não causa erro) |

### API (Application Programming Interface)

Conjunto de protocolos, rotinas e ferramentas para construção de software, definindo como diferentes componentes devem interagir para que sistemas distintos se comuniquem entre si.

**REST** (*Representational State Transfer*): estilo arquitetural para sistemas distribuídos na web. Princípios:

- Comunicação cliente-servidor **sem estado** (*stateless*)
- Uso padrão de **métodos HTTP**
- Recursos identificados por **URIs**
- Representações de dados (como **JSON**)

Referência: Fielding (2000).

### Endpoint

Uma URL específica que fornece acesso a um recurso ou funcionalidade de uma API — o ponto de comunicação entre cliente e servidor.

**Exemplos:**

```text
https://api.exemplo.com/usuarios      → GET: lista todos os usuários
https://api.exemplo.com/usuarios      → POST: adiciona um novo usuário
```

### Servidor backend e web service

- **Servidor backend:** processa requisições, gerencia dados e fornece respostas para clientes (apps, navegadores). Funções principais: armazenar/recuperar dados (banco de dados), executar regras de negócio, fornecer APIs para comunicação.
- **Web service:** serviço acessível via web, que permite comunicação entre sistemas usando HTTP/HTTPS, mesmo entre linguagens ou plataformas diferentes.

### JSON (JavaScript Object Notation)

Formato leve de troca de dados: fácil para humanos lerem e escreverem, e fácil para máquinas interpretarem e gerarem. Baseado em duas estruturas:

- **Objetos:** coleções de pares nome/valor
- **Arrays:** listas ordenadas de valores

**Complemento — exemplo de objeto JSON:**

```json
{
  "id": "1",
  "titulo": "Lembretes",
  "texto": "Comprar leite e pão",
  "criadoEm": "2025-04-29T10:00:00Z"
}
```

---

## 5. Criando uma API REST com Express

**Passo 1 — Inicializar o projeto:** criar uma pasta e abrir no VS Code.

**Passo 2 — Instalar o Express:**

```bash
npm install express
```

**Passo 3 — Instalar o CORS:**

```bash
npm install cors express
```

**Passo 4 — Criar o arquivo `api.js`** com a lógica do servidor.

**Passo 5 — Executar o servidor:**

```bash
node api.js
```

> **CORS** (*Cross-Origin Resource Sharing*) é um mecanismo de segurança que controla o acesso entre domínios diferentes no navegador.

### Render para simular Web Services

Plataforma de hospedagem em nuvem: suporta Node.js, Python e outras linguagens; integração fácil com repositórios Git; *deploy* contínuo automático; planos gratuitos para projetos pequenos; interface simples; escalável; certificado SSL grátis; ideal para APIs e microsserviços. Fonte: [render.com](https://render.com/).

**Benefícios do Render:** *deploy* rápido, configuração simplificada sem terminal, atualizações automáticas via GitHub, ambiente de produção profissional, escalabilidade automática, monitoramento de desempenho, suporte técnico, infraestrutura confiável, perfeito para projetos acadêmicos.

### Publicando a API no Render

1. **Commit do projeto no GitHub:** deixar o projeto disponível em um repositório
2. **Criar conta no Render:** acessar `dashboard.render.com`
3. **Criar novo "Web Service":** clicar em *New* e conectar o repositório do GitHub
4. **Definir comando de start:** em *Build Command*: `node`; em *Start Command*: `node api.js`
5. **Deploy do web service:** após o *deploy*, usar `seu-projeto.onrender.com`

---

## 6. Atividade

1. Criar uma API usando Express, definindo uma rota de consulta de data e hora. Fazer o *deploy* no Render, conectando ao repositório para garantir que a API fique acessível online. Desenvolver uma aplicação *front-end* que consuma essa API e mostre a data e hora na tela.
2. Usar **outro repositório** para separar a API do front. Organizar tudo em um documento com prints do código, da aplicação em funcionamento e dos painéis do Render e Vercel, além dos links dos repositórios no GitHub, e salvar a atividade no GitHub.

---

## Referências

FREEMAN, E.; ROBSON, E. **Modern Web Development**: Building and Deploying with Modern Tools. 1. ed. Sebastopol: O'Reilly Media, 2022.

FIELDING, Roy Thomas. **Architectural styles and the design of network-based software architectures**. 2000. Tese (Doutorado em Ciência da Computação) — University of California, Irvine, 2000.

NEWMAN, S. **Building Microservices**: Designing Fine-Grained Systems. 2. ed. Sebastopol: O'Reilly Media, 2021.

DINIZ, Luciana Mara Freitas et al. Aprendizado Baseado em Projetos em IHC (presencial e remoto): prototipação segundo as heurísticas de Nielsen. In: SIMPÓSIO BRASILEIRO DE FATORES HUMANOS EM SISTEMAS COMPUTACIONAIS (IHC). SBC, 2020. p. 13-18.

GONÇALVES, Rodrigo Franco et al. Uma proposta de processo de produção de aplicações Web. **Production**, v. 15, p. 376-389, 2005.

LUCASSEN, Garm et al. The use and effectiveness of user stories in practice. In: REQUIREMENTS ENGINEERING: FOUNDATION FOR SOFTWARE QUALITY, 22., 2016, Gothenburg. **Proceedings** [...]. Springer International Publishing, 2016. p. 205-222.

SALINAS, C.; SEDEÑO, J.; CUARESMA, M.; RISOTO, M. Agile, Web Engineering and Capability Maturity Model Integration: A systematic literature review. **Information and Software Technology**, v. 71, p. 92-107, 2016. DOI: 10.1016/J.INFSOF.2015.11.002.

NGUYEN, Hong-Thu Thi. Website Builder as an Assistive Technology Tool for Reflection, Collaboration and Skills Development in Learning ESP. **Journal of Learning for Development**, v. 11, n. 1, p. 138-150, 2024.

> Nota: o slide cita Rockford (2008), mas a referência completa não consta na lista da aula.
