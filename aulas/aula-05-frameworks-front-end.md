# Aula 05 — Introdução a Frameworks Front-end

> Prof. Me. Deivison S. Takatu

## Sumário

1. [Frameworks front-end](#1-frameworks-front-end)
2. [Framework x Biblioteca](#2-framework-x-biblioteca)
3. [Exemplos de frameworks](#3-exemplos-de-frameworks)
4. [Características](#4-características-dos-frameworks-front-end)
5. [Introdução ao React](#5-introdução-ao-react)
6. [Node.js e NPM](#6-nodejs-e-npm)
7. [Criando um projeto React](#7-criando-um-projeto-react)
8. [Atividade](#8-atividade)

---

## 1. Frameworks front-end

Conjunto de **ferramentas, bibliotecas e convenções** que padronizam o desenvolvimento de interfaces web, fornecendo uma estrutura pré-definida.

| Sem framework (Vanilla JS) | Com framework |
|---|---|
| Código manual, difícil de manter, repetitivo | Componentes reutilizáveis, estado gerenciado, atualizações eficientes |

Referência: Banks; Porcello (2017).

**Complemento — o mesmo contador, sem e com framework:**

Sem framework (Vanilla JS): você atualiza a tela manualmente.

```html
<h2 id="total">0</h2>
<button id="btn">+1</button>

<script>
  let total = 0;
  document.getElementById('btn').addEventListener('click', () => {
    total++;
    document.getElementById('total').textContent = total; // atualização manual do DOM
  });
</script>
```

Com React: você só muda o **estado**, e a tela se atualiza sozinha.

```jsx
import { useState } from 'react';

function Contador() {
  const [total, setTotal] = useState(0);

  return (
    <div>
      <h2>{total}</h2>
      <button onClick={() => setTotal(total + 1)}>+1</button>
    </div>
  );
}

export default Contador;
```

**Por que usar:**

- **Produtividade:** soluções prontas para roteamento, estado e renderização
- **Melhores práticas:** código organizado em componentes
- **Manutenção facilitada:** Virtual DOM (React), *Change Detection* (Angular)
- **Comunidade e suporte:** documentação extensa, plugins e soluções prontas

---

## 2. Framework x Biblioteca

| Framework | Biblioteca |
|---|---|
| **Controla o fluxo** (inversão de controle) | **Você controla** quando chamar |
| Exige estrutura definida | Flexível, sem imposições |
| Ex.: Angular, Vue | Ex.: React, jQuery |

**Exemplo:**

- Biblioteca: você chama `ReactDOM.render()` quando quiser
- Framework: o Angular decide quando renderizar os componentes

**Inversão de controle, em palavras simples:** na biblioteca, o **seu código** chama a ferramenta. No framework, é o **framework** que chama o seu código no momento certo (você "preenche os espaços" da estrutura que ele define).

---

## 3. Exemplos de frameworks

- **React:** criado pelo Facebook; tecnicamente é uma **biblioteca** JavaScript para construir interfaces, com componentes reutilizáveis
- **Angular:** desenvolvido pelo Google; framework **completo** para SPAs (*Single Page Applications*)
- **Vue.js:** framework **progressivo**, fácil de adaptar conforme a aplicação cresce

> A escolha impacta desempenho, escalabilidade, manutenção e experiência do usuário. Considere complexidade do projeto, curva de aprendizado, desempenho e suporte da comunidade. Comparativo: [StackShare](https://stackshare.io/stackups).

---

## 4. Características dos frameworks front-end

- **Estrutura de código organizada:** separação clara de HTML, CSS e JS
- **Componentização:** componentes independentes e reutilizáveis, que encapsulam lógica e apresentação
- **Programação reativa:** a UI é atualizada automaticamente quando o estado muda, sem manipular o DOM manualmente
- **Build e bundling:** minificar, transpilar e combinar arquivos
- **Sistema de rotas:** SPAs com navegação suave, sem recarregar a página
- **Integração com APIs:** chamadas assíncronas e sincronização de dados
- **Documentação e comunidade**
- **Padrões de design e acessibilidade**
- **Suporte a testes:** unitários e de integração

Referência: Rahat et al. (2023).

---

## 5. Introdução ao React

- Biblioteca desenvolvida pelo **Facebook em 2013**, muito usada para Web Apps e interfaces dinâmicas
- Requer conhecimento prévio de **HTML e JavaScript**
- Arquitetura baseada em **componentes** e uso do **Virtual DOM**

Referência: Aggarwal et al. (2018).

### Conceitos fundamentais

**Hooks:**

- `useState`: gerencia o estado de um componente funcional
- `useEffect`: lida com efeitos colaterais (ex.: chamadas de API)

**JSX (diferenças em relação ao HTML):**

- Usa `{}` para expressões JavaScript
- Atributos em *camelCase* (`className` em vez de `class`)
- Tags sempre fechadas (`<img />`)

**Gerenciamento de estado:**

- **Context API:** simples, para estados menores
- **Redux:** para estados complexos e compartilhados globalmente

### Exemplos de código

**Complemento:** para fixar os conceitos acima.

**JSX x HTML:**

```jsx
// HTML
<label for="nome">Nome</label>
<input type="text" id="nome">
<img src="foto.png">

// JSX
<label htmlFor="nome">Nome</label>
<input type="text" id="nome" />
<img src="foto.png" alt="Foto" />
```

No JSX, `class` vira `className`, `for` vira `htmlFor`, e toda tag precisa ser fechada.

**`useState`:** guarda um valor e devolve uma função para alterá-lo.

```jsx
const [nome, setNome] = useState('');   // valor inicial: texto vazio

<input value={nome} onChange={(e) => setNome(e.target.value)} />
<p>Olá, {nome}!</p>
```

**`useEffect`:** executa um efeito colateral, como buscar dados de uma API. Exemplo com o buscador de CEP da atividade:

```jsx
import { useState, useEffect } from 'react';

function BuscadorCep() {
  const [cep, setCep] = useState('');
  const [endereco, setEndereco] = useState(null);

  useEffect(() => {
    if (cep.length !== 8) return;               // só busca com 8 dígitos

    fetch(`https://viacep.com.br/ws/${cep}/json/`)
      .then((resposta) => resposta.json())
      .then((dados) => setEndereco(dados));
  }, [cep]);                                     // roda de novo quando o cep mudar

  return (
    <div>
      <input value={cep} onChange={(e) => setCep(e.target.value)} placeholder="Digite o CEP" />
      {endereco && <p>{endereco.logradouro}, {endereco.bairro} - {endereco.localidade}</p>}
    </div>
  );
}
```

O array no final (`[cep]`) é a **lista de dependências**: o efeito só roda quando algum item dela muda. Com `[]`, roda apenas uma vez, quando o componente aparece na tela.

**Usando um componente dentro de outro (`App.js`):**

```jsx
import Contador from './Contador';
import BuscadorCep from './BuscadorCep';

function App() {
  return (
    <div>
      <h1>Meu projeto</h1>
      <Contador />
      <BuscadorCep />
    </div>
  );
}

export default App;
```

### DOM e Virtual DOM

- **DOM:** representação em árvore da estrutura da página, que o JavaScript pode alterar
- **Virtual DOM:** cópia do DOM usada pelo React. Quando algo muda, o React atualiza a cópia, **compara** com o DOM real e aplica **só as diferenças**, o que torna o processo mais rápido

---

## 6. Node.js e NPM

**Node.js:** ambiente de execução JavaScript no servidor (backend). Permite usar a **mesma linguagem** no servidor e no navegador.

**Instalação:** baixar em [nodejs.org/en/download](https://nodejs.org/en/download), executar o instalador e testar:

```bash
node --version
```

**NPM (Node Package Manager):** gerenciador de pacotes, instalado junto com o Node.js.

- Instala, atualiza e remove bibliotecas e frameworks
- O `package.json` registra as dependências do projeto
- Em um projeto clonado, basta rodar `npm install` para baixar tudo

---

## 7. Criando um projeto React

```bash
# 1. Criar o projeto
npx create-react-app meu-projeto-react

# 2. Entrar na pasta
cd meu-projeto-react

# 3. Abrir no VS Code
code .

# 4. Iniciar o servidor local
npm start
```

- `npx`: executor de pacotes npm que vem com o Node.js
- `create-react-app`: pacote oficial que gera o projeto (Webpack, Babel, servidor local, scripts de build/teste e estrutura de pastas)

> **Complemento:** o `create-react-app` é o comando usado na disciplina, mas a equipe do React o descontinuou em 2025. Hoje é comum criar projetos com o **Vite**: `npm create vite@latest meu-projeto -- --template react`. A estrutura e os conceitos (componentes, hooks, JSX) são os mesmos.

Referência: Banks; Porcello (2017).

### Estrutura de pastas e arquivos

| Item | Função |
|---|---|
| `node_modules/` | Pacotes instalados (`npm i` instala as dependências) |
| `public/` | HTML, JSON, imagens |
| `src/` | Arquivos JS React do projeto |
| `.gitignore` | Arquivos e diretórios ignorados pelo Git (ex.: senhas) |
| `package.json` / `package-lock.json` | Informações, scripts e dependências do projeto |

**Dentro de `src/`:**

| Arquivo | Função |
|---|---|
| `index.js` | Ponto de entrada; renderiza o `App` no DOM |
| `App.js` | Componente raiz da aplicação |
| `App.css` | Estilos do componente `App` |
| `index.css` | Estilos globais |

**Publicar no GitHub:** VS Code → *Publicar Branch* → login no GitHub → escolher público ou privado → conferir o repositório.

---

## 8. Atividade

1. Criar um projeto React com um **cabeçalho** listando as funcionalidades: To-Do List, Contador de Cliques, Jogo da Velha, Calculadora e Buscador de CEP.
2. Fazer commit no GitHub e **deploy no Vercel**, conectando o repositório.
3. Documentar os elementos criados, incluindo a escolha da estilização.
4. Organizar em um documento: etapas realizadas, prints, links do GitHub e do Vercel; submeter o arquivo.

---

## Referências

> Os slides citam as obras abaixo no texto, mas não trazem a referência completa na lista da aula: Banks; Porcello (2017), Rahat et al. (2023) e Aggarwal et al. (2018). Complete antes de usar em trabalho ABNT.

- NODE.JS. Download. Disponível em: https://nodejs.org/en/download.
- STACKSHARE. Stackups. Disponível em: https://stackshare.io/stackups.
