# Aula 03 — Introdução ao Versionamento e Deploy

> Prof. Me. Deivison S. Takatu

## Sumário

1. [Versionamento x Backup](#1-versionamento-x-backup)
2. [Introdução ao versionamento](#2-introdução-ao-versionamento)
3. [Versionamento Semântico (SemVer)](#3-versionamento-semântico-semver)
4. [Git](#4-git)
5. [Tags](#5-tags-no-git)
6. [Branches, merge e conflitos](#6-branches-merge-e-conflitos)
7. [Boas práticas](#7-boas-práticas-git)
8. [Deploy e hospedagem](#8-deploy-e-hospedagem)
9. [Atividade](#9-atividade)
10. [Referências](#referências)

---

## 1. Versionamento x Backup

| Versionamento | Backup |
|---|---|
| Histórico de cada alteração | Cópia pontual do estado atual |
| Registra quem, quando e por quê mudou | Sem rastreio de autoria |
| Permite colaboração simultânea | Arquivo único, sem *merge* |
| Reversão granular | Restauração total apenas |

**Sem versionamento (o caos):** arquivos como `versao_final_agora_sim2.zip`, código perdido, conflito entre devs e nenhum histórico.

**Benefícios do versionamento:**

- **Trabalho simultâneo:** vários devs no mesmo projeto sem sobrescrever o trabalho uns dos outros
- **Menos retrabalho:** conflitos identificados cedo
- **Auditoria e rastreabilidade:** quem alterou o quê, quando e por quê
- **Recuperação de versões:** voltar a qualquer ponto do histórico

---

## 2. Introdução ao versionamento

Processo de atribuir um **identificador único** a cada versão de um documento ou software.

- Pode ser numérico (`v1.0`, `v1.1`, `v2.0`) ou baseado em datas (`2023-10-01`)
- Registra o que mudou, por quem e quando
- Garante rastreabilidade e auditoria
- Facilita organização, colaboração e recuperação de versões anteriores

**Importância:**

| Aspecto | O que oferece |
|---|---|
| Controle de mudanças | Vários colaboradores no projeto; evita perda de trabalho |
| Histórico e auditabilidade | Registro de todas as modificações; útil para conformidade |
| Recuperação de dados | Reverter para versões anteriores |
| Colaboração eficiente | Uso de *branches* sem afetar a principal |
| Gerenciamento da qualidade | Testar antes da versão final |
| Aprimoramento contínuo | Analisar a evolução do projeto |
| Integração com outras ferramentas | Gestão de projetos e integração contínua |

Referência: Tate; Louth (2022).

---

## 3. Versionamento Semântico (SemVer)

Padrão **`MAJOR.MINOR.PATCH`** (ex.: `2.1.3`):

| Parte | Quando incrementar | Exemplo |
|---|---|---|
| **MAJOR** | Mudança **incompatível** com versões anteriores | `2.0.0` |
| **MINOR** | Nova funcionalidade **retrocompatível** | `1.1.0` |
| **PATCH** | Correção de bug, sem alterar a API | `1.0.1` |

- `1.0.0` marca o lançamento público estável
- Versões `0.x.x` indicam desenvolvimento inicial

**Exemplo prático:**

```text
1.0.0 → primeira versão estável
1.1.0 → funcionalidade compatível adicionada
1.1.1 → correção de bug
2.0.0 → mudança incompatível
```

**Vantagens:** facilita a gestão de dependências, dá clareza a devs e usuários e ajuda na manutenção e previsibilidade.

**Exemplos de alterações no código:**

- **Bug Fix:** correção de erros
- **New Feature:** nova funcionalidade
- **Feature Enhancement:** melhoria de funcionalidade existente
- **Refactoring:** reorganizar o código para ficar mais limpo e eficiente
- **Performance:** otimização de velocidade e eficiência
- **Security Patch:** correção de vulnerabilidades
- **Dependency Update:** atualização de bibliotecas e frameworks
- **Adding Tests:** inclusão de testes automatizados

---

## 4. Git

**O que é:** sistema de controle de versão de arquivos, instalado no computador e usado via linha de comando.

**O que faz:**

- Sincroniza com repositórios online (baixar e enviar código)
- Registra versões do projeto, permitindo acompanhar mudanças e restaurar versões anteriores

Referência: Loeliger; McCullough (2021).

### Instalação

1. Baixar em [git-scm.com/downloads](https://git-scm.com/downloads) a versão do seu sistema operacional
2. Executar o instalador (*Next > Next > Install*)
3. Testar no Prompt de Comando:

```bash
git --version
```

4. Configurar usuário e e-mail, se solicitado:

```bash
git config --global user.name "<Nome>"
git config --global user.email "<Email>"
```

5. No VS Code, abrir a aba **Controle de Código-Fonte** (terceiro ícone à esquerda); instalar o Git se solicitado e reabrir o VS Code

### Criando um repositório no VS Code

1. Criar uma pasta (ex.: `HTML_Teste`) e abrir no VS Code
2. Criar um arquivo `index.html`
3. Em **Controle de Código-Fonte**, clicar em **Inicializar Repositório**
4. Escrever uma mensagem de commit e clicar em **Confirmar (Commit)**

### Ciclo básico de comandos

**Complemento:** o dia a dia com Git, em ordem.

```bash
git init                   # cria um repositório na pasta atual
git status                 # mostra o que mudou e o que está pronto para commit
git add .                  # coloca as alterações na área de preparação (staging)
git commit -m "mensagem"   # grava as alterações no histórico
git log --oneline          # lista o histórico resumido
git push origin main       # envia os commits ao GitHub
git pull                   # baixa as novidades do GitHub
git clone <url>            # copia um repositório do GitHub para o seu computador
```

Caminho de uma alteração:

```text
pasta de trabalho --add--> staging --commit--> repositório local --push--> GitHub
```

**Mensagens de commit:** um padrão comum é começar com um prefixo que diz o tipo da mudança, como `feat:` (nova funcionalidade), `fix:` (correção) e `docs:` (documentação). Exemplo: `fix: corrige link quebrado no menu`.

### Publicando no GitHub

1. Clicar em **Publicar Branch**
2. Fazer login no GitHub
3. Escolher repositório **público** ou **privado**
4. Conferir no perfil do GitHub, em *Repositórios*, se o projeto aparece

---

## 5. Tags no Git

Marcadores para identificar pontos específicos do histórico, como versões estáveis (`v1.0`, `v2.0`). Uso comum: marcar *releases*.

**Tipos:**

- **Leve (lightweight):** apenas um nome apontando para um commit
- **Anotada (annotated):** guarda data, autor e mensagem

**Comandos:**

```bash
git tag                    # lista as tags
git tag 1.0.0              # cria uma tag (ex.: no primeiro commit)
git push origin 1.0.0      # envia a tag ao GitHub
```

Assim, a cada alteração fica mais fácil descrever as mudanças e manter a sequência de versões.

**Complemento — tag leve x anotada, na prática:**

```bash
git tag v1.0.0                                   # leve: só o nome
git tag -a v1.0.0 -m "Primeira versão estável"   # anotada: com autor, data e mensagem
git show v1.0.0                                  # mostra os dados da tag
git push origin --tags                           # envia todas as tags de uma vez
```

---

## 6. Branches, merge e conflitos

**Branches:** ramificações do código para trabalhar em funcionalidades ou correções sem afetar a versão principal.

| Branch | Função |
|---|---|
| `main` / `master` | Versão estável do projeto |
| `develop` | Integrar novas funcionalidades antes de ir para a `main` |
| `feature` | Desenvolver uma funcionalidade específica |
| `hotfix` | Corrigir um bug urgente |

**Merge:** une duas branches, integrando as mudanças de uma na outra.

**Conflitos:** ocorrem quando duas branches alteram a mesma parte do código; exigem resolução manual.

**Boas práticas no merge:**

- Atualize sua branch antes de fazer *merge*
- Resolva conflitos com cuidado

**Complemento — comandos de branch e merge:**

```bash
git branch                     # lista as branches (a atual vem com *)
git switch -c feature/login    # cria a branch e já muda para ela
# ...edita, git add, git commit...
git switch main                # volta para a main
git merge feature/login        # traz as mudanças da feature para a main
git branch -d feature/login    # apaga a branch já integrada
```

(Em versões mais antigas do Git, `git switch -c` equivale a `git checkout -b`.)

**Complemento — como é um conflito e como resolver:** se duas branches mudaram a mesma linha, o Git para o merge e marca o arquivo assim:

```text
<<<<<<< HEAD
<h1>Bem-vindo ao site</h1>
=======
<h1>Olá, seja bem-vindo!</h1>
>>>>>>> feature/novo-titulo
```

- Entre `<<<<<<< HEAD` e `=======` está a versão da branch atual
- Entre `=======` e `>>>>>>>` está a versão que está sendo integrada

Para resolver:

1. Abra o arquivo e **escolha** o que fica (uma das versões, ou uma mistura)
2. **Apague** as linhas `<<<<<<<`, `=======` e `>>>>>>>`
3. Rode `git add <arquivo>` e depois `git commit` para concluir o merge

**Situação-problema (exemplo do slide):** o app em produção fica na `main`. Surgem um novo recurso e um bug crítico. A equipe cria uma branch de *feature* e outra de *hotfix*, testa e integra ambas à `main`. **Benefício:** a versão estável não é afetada durante o desenvolvimento.

---

## 7. Boas práticas Git

- **Commits pequenos e frequentes:** facilitam identificar problemas e reverter mudanças
- **Mensagens de commit claras:** descrever o que mudou e por quê
- **Uso de branches:** manter a principal estável; novas funcionalidades e correções em branches próprias
- **Testes automatizados:** garantir que o código funciona antes do *merge*

---

## 8. Deploy e hospedagem

**Deploy:** processo de colocar a aplicação em **produção**, tornando-a acessível aos usuários finais.

**Objetivo:** garantir que o software funcione corretamente em produção.

**Etapas comuns:** compilação → configuração do ambiente → testes finais → publicação.

**Ambientes:**

| Ambiente | Descrição |
|---|---|
| Desenvolvimento | Ambiente local do dev; erros são esperados |
| Staging | Cópia fiel da produção, para testes finais |
| Produção | Ambiente real, acessado pelos usuários |

### Vercel

- **Hospedagem simplificada:** focada em sites estáticos e aplicações modernas
- **Integração com Git:** GitHub, GitLab e Bitbucket, com deploy automático a cada *push*
- **Frameworks modernos:** Next.js, Nuxt.js, React, Vue etc.
- **Deploys instantâneos**, com *rollback*
- **Serverless Functions:** backend sem gerenciar servidores
- **CDN global:** baixa latência
- Foco em performance, escalabilidade automática e segurança

**Complemento — passo a passo do deploy na Vercel:**

1. Entrar em [vercel.com](https://vercel.com) com a conta do GitHub
2. **Add New → Project**
3. Escolher o repositório em **Import Git Repository**
4. Conferir o *Framework Preset* (a Vercel costuma detectar sozinha) e clicar em **Deploy**
5. Receber o link público do site

A partir daí, cada `git push` na `main` gera um **novo deploy automático**.

---

## 9. Atividade

1. Criar um repositório no GitHub com um projeto simples (página HTML básica). Versionar com Git, usar **tags** para versões estáveis, personalizar e fazer **deploy no Vercel** conectado ao repositório.
2. Documentar todo o processo (justificativa do design, personalizações, passos de versionamento e deploy), com **prints** e **links** do repositório e do site no Vercel, e submeter o arquivo.

---

## Referências

TATE, B.; LOUTH, F. **Version Control with Git**: Powerful Tools and Techniques for Collaborative Software Development. Sebastopol: O'Reilly Media, 2022.

HODSON, R. **Continuous Delivery and DevOps**: A Quickstart Guide. 2. ed. Birmingham: Packt Publishing, 2023.

FREEMAN, E.; ROBSON, E. **Modern Web Development**: Building and Deploying with Modern Tools. 1. ed. Sebastopol: O'Reilly Media, 2022.

> Nota: o slide cita Loeliger; McCullough (2021), mas a referência completa não consta na lista da aula.
