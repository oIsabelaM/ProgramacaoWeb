# Aula 06 — Atividade com Projetos Front-end

> Prof. Me. Deivison S. Takatu

## Sumário

1. [Node.js e NPM](#1-nodejs-e-npm)
2. [React](#2-react)
3. [Angular](#3-angular)
4. [Vue](#4-vue)
5. [Importação de projetos](#5-importação-de-projetos)
6. [Comparativo](#6-comparativo-rápido)
7. [Atividade](#7-atividade)

---

## 1. Node.js e NPM

- **Node.js:** ambiente de execução JavaScript no servidor; permite usar a mesma linguagem no backend e no navegador. Instalação em [nodejs.org/en/download](https://nodejs.org/en/download).
- **NPM:** gerenciador de pacotes instalado com o Node.js. O `package.json` registra as dependências; `npm install` baixa todas.

Testar a instalação:

```bash
node --version
```

---

## 2. React

**Requisitos:**

- Node.js instalado
- [JSX](https://react.dev/learn/writing-markup-with-jsx) (sintaxe de HTML dentro do JavaScript)
- [Hooks](https://react.dev/reference/react/hooks) (`useState`, `useEffect` etc.)

**Destaques:**

- **Flexibilidade:** não impõe estrutura rígida
- **Grande ecossistema:** Redux, React Router, Next.js
- **Componentização:** reutilização eficiente de código
- **Virtual DOM:** performance otimizada
- **Comunidade ativa**

**Criando o projeto:**

```bash
npx create-react-app meu-projeto-react
cd meu-projeto-react
code .
npm start
```

**Estrutura:**

| Item | Função |
|---|---|
| `node_modules/` | Pacotes instalados (`npm i` instala as dependências) |
| `public/` | HTML, JSON, imagens |
| `src/` | Código React do projeto |
| `.gitignore` | Arquivos ignorados pelo Git |
| `package.json` / `package-lock.json` | Dependências e scripts |
| `src/index.js` | Ponto de entrada; renderiza o `App` no DOM |
| `src/App.js` | Componente raiz |
| `src/App.css` | Estilos do `App` |
| `src/index.css` | Estilos globais |

**Complemento — um componente React completo (`src/Contador.js`):**

```jsx
import { useState } from 'react';

function Contador() {
  const [total, setTotal] = useState(0);

  return (
    <div>
      <h2>Contador: {total}</h2>
      <button onClick={() => setTotal(total + 1)}>+1</button>
    </div>
  );
}

export default Contador;
```

Para exibir, importe e use `<Contador />` dentro do `App.js`.

> O `create-react-app` foi descontinuado em 2025; a alternativa atual é o Vite (`npm create vite@latest`). Veja a nota na Aula 05.

---

## 3. Angular

**Requisitos:**

- Node.js instalado
- Programação orientada a objetos (POO)

**Destaques:**

- **Framework completo:** roteamento, HTTP client, injeção de dependências
- **TypeScript nativo:** melhor suporte a tipos e escalabilidade
- **Arquitetura MVC:** separação clara de responsabilidades
- **CLI poderosa:** gera componentes, serviços etc. automaticamente
- **Performance:** *Change Detection* eficiente

### Conceitos fundamentais

| Conceito | Descrição |
|---|---|
| Componentes | Estrutura com `@Component` (HTML + CSS + TypeScript) |
| Módulos | `@NgModule`: organiza o app em blocos funcionais |
| Serviços | Lógica reutilizável com `@Injectable` |
| Data binding | `[(ngModel)]` (two-way binding) e `{{ }}` (interpolação) |
| Injeção de dependência | Hierarquia de *providers* |
| Roteamento | `RouterModule` para navegar entre views |

### Criando o projeto

```bash
# 1. Instalar o Angular CLI globalmente
npm install -g @angular/cli

# 2. Criar o projeto
ng new meu-app-angular

# 3. Entrar na pasta
cd meu-app-angular

# 4. Abrir no VS Code
code .

# 5. Iniciar o servidor de desenvolvimento
ng serve
```

**Angular CLI:** ferramenta de linha de comando para criar, gerenciar e construir projetos Angular.

### Estrutura

| Item | Função |
|---|---|
| `node_modules/` | Pacotes e dependências |
| `public/` | Arquivos estáticos |
| `src/` | Código-fonte principal |
| `.angular/` | Cache e configurações temporárias de build (gerada pelo CLI) |
| `.vscode/` | Configurações do VS Code |
| `.gitignore` | Arquivos ignorados pelo Git |
| `.editorconfig` | Padroniza a formatação entre editores |
| `README.md` | Documentação do projeto |
| `angular.json` | Configuração principal (build, testes, estilos globais) |
| `tsconfig.json` | Regras base do TypeScript |
| `tsconfig.app.json` | Configuração do TypeScript para a aplicação |
| `tsconfig.spec.json` | Configuração do TypeScript para os testes |

**Dentro de `src/`:**

| Item | Função |
|---|---|
| `app/` | Componentes, módulos, serviços e outros arquivos principais |
| `index.html` | Ponto de entrada HTML; renderiza o componente raiz via `<app-root>` |
| `main.ts` | Inicializa o módulo raiz e renderiza a aplicação no DOM |
| `main.server.ts` | Ponto de entrada do Angular Universal (SSR) |
| `server.ts` | Configuração do servidor para SSR |
| `styles.css` | Estilos globais |

**Complemento — um componente Angular (`contador.component.ts`):**

```ts
import { Component } from '@angular/core';
import { FormsModule } from '@angular/forms';

@Component({
  selector: 'app-contador',
  standalone: true,
  imports: [FormsModule],
  template: `
    <h2>Contador: {{ total }}</h2>
    <button (click)="incrementar()">+1</button>

    <input [(ngModel)]="nome" placeholder="Seu nome" />
    <p>Olá, {{ nome }}!</p>
  `,
})
export class ContadorComponent {
  total = 0;
  nome = '';

  incrementar() {
    this.total++;
  }
}
```

- `{{ total }}`: interpolação (mostra o valor na tela)
- `(click)`: evento de clique
- `[(ngModel)]`: two-way binding (input e variável sempre sincronizados)
- Para usar: `<app-contador />` em outro componente, importando-o na lista `imports`

> Em versões recentes, o `ng new` já cria componentes *standalone* (sem `AppModule`). A aula apresenta a abordagem com módulos (`@NgModule`), que continua válida em projetos existentes.

---

## 4. Vue

**Requisitos:**

- Node.js instalado
- JavaScript/TypeScript
- Programação reativa e baseada em componentes ([guia](https://vuejs.org/guide/introduction.html))

**Destaques:**

- **Progressivo:** pode ser adotado aos poucos, de pequenas partes a SPAs complexas
- **Reatividade eficiente:** automática e performática
- **Single-File Components (SFC):** HTML, CSS e JS em um único arquivo `.vue`
- **Curva de aprendizado suave**
- **Performance otimizada:** Virtual DOM eficiente e tamanho reduzido

**Criando o projeto:**

```bash
# 1. Criar o projeto
npm create vue@latest

# 2. Entrar na pasta
cd meu-projeto-vue

# 3. Instalar as dependências
npm install

# 4. Abrir no VS Code
code .

# 5. Iniciar o servidor de desenvolvimento
npm run dev
```

**Estrutura:**

| Item | Função |
|---|---|
| `node_modules/` | Pacotes e dependências |
| `public/` | Arquivos estáticos que **não** passam pelo build do Vite (ex.: `favicon.ico`, `robots.txt`) |
| `src/` | Código-fonte principal |
| `.vscode/` | Configurações do VS Code |
| `.gitignore` | Arquivos ignorados pelo Git |
| `package.json` / `package-lock.json` | Dependências e scripts |
| `vite.config.js` | Configurações do Vite (build, plugins, proxies) |
| `index.html` | Único HTML da SPA; contém a `div#app` onde o Vue é injetado |

**Dentro de `src/`:**

| Item | Função |
|---|---|
| `assets/` | Imagens, fontes, CSS global (processados pelo Vite) |
| `components/` | Componentes reutilizáveis (ex.: `Button.vue`, `Header.vue`) |
| `App.vue` | Componente raiz; define a estrutura inicial e importa outros componentes |
| `main.js` | Ponto de entrada; monta o app no DOM e configura plugins globais |

**Complemento — um componente Vue (`src/components/Contador.vue`):**

```vue
<script setup>
import { ref } from 'vue'

const total = ref(0)
</script>

<template>
  <h2>Contador: {{ total }}</h2>
  <button @click="total++">+1</button>
</template>

<style scoped>
button {
  padding: 0.5rem 1rem;
}
</style>
```

Este é um **Single-File Component (SFC)**: lógica (`<script>`), HTML (`<template>`) e CSS (`<style>`) no mesmo arquivo `.vue`. O `scoped` faz o estilo valer só para este componente. Para usar, importe-o no `App.vue` e escreva `<Contador />`.

---

## 5. Importação de projetos

Encontrar **projetos modelo** com o framework desejado acelera o desenvolvimento. A comunidade open source oferece muitos projetos gratuitos, personalizáveis e com boas práticas.

**Onde pesquisar:**

| Ferramenta | Observação |
|---|---|
| GitHub (busca de repositórios) | Usar `git clone <url>` |
| Vercel (busca de templates) | Permite baixar apenas uma parte do repositório |
| [CodeSandbox](https://codesandbox.io/) (busca de templates) | — |

**Complemento — fluxo para importar um template e publicá-lo em um repositório seu:**

```bash
git clone https://github.com/usuario/template.git meu-projeto
cd meu-projeto
npm install                     # instala as dependências
npm run dev                     # ou npm start / ng serve (veja o README do template)
```

Depois de alterar o projeto, para enviá-lo ao **seu** (quarto) repositório:

```bash
git remote remove origin        # desliga o repositório original
git remote add origin https://github.com/SEU-USUARIO/NOVO-REPO.git
git add .
git commit -m "feat: personaliza template"
git push -u origin main
```

**Deploy de cada projeto na Vercel:** *Add New → Project*, escolher o repositório e clicar em *Deploy*. A Vercel detecta React, Angular ou Vue automaticamente; se o build falhar, confira o *Framework Preset* na tela de configuração.

---

## 6. Comparativo rápido

| | React | Angular | Vue |
|---|---|---|---|
| Tipo | Biblioteca | Framework completo | Framework progressivo |
| Linguagem base | JavaScript (JSX) | TypeScript | JavaScript/TypeScript |
| Criar projeto | `npx create-react-app` | `ng new` | `npm create vue@latest` |
| Iniciar servidor | `npm start` | `ng serve` | `npm run dev` |
| Ponto de entrada | `index.js` | `main.ts` | `main.js` |
| Componente raiz | `App.js` | `AppModule` / `<app-root>` | `App.vue` |

---

## 7. Atividade

1. Criar **três projetos** (React, Angular e Vue), fazer alterações iniciais no código e versionar cada um em **repositórios diferentes** no GitHub.
2. Pesquisar um **template** feito com um dos frameworks, importar, alterar e fazer commit em um **quarto repositório**.
3. Fazer o **deploy de cada um dos quatro** na Vercel.
4. Documentar tudo em **um único arquivo**: descrições, prints e links dos repositórios (GitHub) e dos projetos (Vercel).
