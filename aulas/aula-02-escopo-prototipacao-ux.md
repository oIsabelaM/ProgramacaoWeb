# Aula 02 — Definição de escopo, prototipação e UX

> Prof. Me. Deivison S. Takatu

## Sumário

1. [Tipos de aplicações web](#1-tipos-de-aplicações-web)
2. [Escopo e backlog do projeto](#2-escopo-e-backlog-do-projeto)
3. [Planejamento e gestão do backlog](#3-planejamento-e-gestão-do-backlog)
4. [Wireframes](#4-wireframes-estruturando-o-site)
5. [Ferramentas de prototipação](#5-ferramentas-de-prototipação)
6. [Atividade](#6-atividade)
7. [Referências](#referências)

---

## 1. Tipos de aplicações web

A classificação varia conforme a referência, mas, por **propósito**, os exemplos comuns são:

- Institucional
- Blog
- E-commerce
- Landing Page
- Plataforma

**Sitemap:** mapa da estrutura do site (exemplo feito no Miro) — Gonçalves et al. (2005).

**Análise da arquitetura do site:** ferramenta [Octopus.do](https://octopus.do/).

---

## 2. Escopo e backlog do projeto

**Pontos principais:**

- Importância de definir o escopo **no início** do projeto web
- Elementos de um escopo bem definido
- Documentação e alinhamento com *stakeholders*
- Agilidade na gestão do backlog

Referência: Salinas et al. (2016).

### Exemplo de escopo

Site institucional para a empresa XYZ, com o objetivo de:

- apresentar a identidade, produtos e serviços da empresa;
- facilitar o contato com clientes.

**Conteúdo:** homepage atrativa, seção sobre a história da marca, blog (dicas e novidades) e formulário de contato.

**Requisitos:** design responsivo (mobile e desktop), navegação intuitiva (usabilidade e acessibilidade).

**Tecnologias:** HTML, CSS, JavaScript e um CMS para gestão de conteúdo.

**Complemento — elementos de um escopo bem definido:**

| Elemento | O que responde | Exemplo (site da XYZ) |
|---|---|---|
| Objetivo | Por que o projeto existe? | Apresentar a empresa e facilitar o contato |
| Entregas | O que será entregue? | Homepage, "Sobre", blog e formulário |
| Requisitos funcionais | O que o sistema **faz**? | Enviar mensagem pelo formulário |
| Requisitos não funcionais | Como ele deve se comportar? | Responsivo, acessível, carregamento rápido |
| Fora do escopo | O que **não** será feito? | Loja virtual, área de login |
| Prazos e restrições | Quando e com quais limites? | 8 semanas, equipe de 4 pessoas |
| *Stakeholders* | Quem decide ou é afetado? | Cliente (XYZ), equipe, visitantes |

> *Stakeholder* é qualquer pessoa ou grupo interessado no projeto ou afetado por ele. Documentar o escopo e alinhá-lo com essas pessoas evita o clássico "eu achei que também incluía...".

---

## 3. Planejamento e gestão do backlog

**Objetivos:**

- Facilitar a comunicação entre equipe e cliente
- Melhorar a experiência do usuário desde o início
- Definir uma estrutura clara para o desenvolvimento
- Utilizar *User Stories*

Referência: Lucassen et al. (2016).

### User Story

Formato:

> **Como** (quem?), **eu quero** (o que?) **para** (por quê?).

Exemplo: *como visitante do site, quero acessar a página "Sobre" para conhecer a história, os valores e a missão da empresa, avaliando sua credibilidade e seus diferenciais.*

**Complemento — mais exemplos, no mesmo formato:**

- *Como* visitante, *eu quero* preencher um formulário de contato *para* pedir um orçamento sem precisar ligar.
- *Como* leitor do blog, *eu quero* ver os posts mais recentes na página inicial *para* acompanhar as novidades da empresa.
- *Como* administrador do site, *eu quero* publicar posts pelo CMS *para* atualizar o conteúdo sem mexer no código.

**Como saber se uma story está boa?** Ela deve ser curta, focada em **um** objetivo do usuário e ter um resultado que dê para testar (ex.: "o formulário envia e mostra uma mensagem de confirmação").

### Gestão de tasks: Kanban

- Quadro visual com colunas (ex.: A fazer, Em andamento, Concluído)
- Método colaborativo e prático
- Funciona como um tipo de documentação do projeto
- Ferramenta usada na atividade: **Trello**

**Complemento — exemplo de quadro Kanban:**

| A fazer | Em andamento | Concluído |
|---|---|---|
| Wireframe do blog | Página "Sobre" | Definir escopo |
| Formulário de contato | Paleta de cores | Pesquisar concorrentes |

Cada linha é um **cartão** (uma tarefa). Ao avançar o trabalho, o cartão muda de coluna, e o quadro mostra o andamento do projeto de relance.

---

## 4. Wireframes: estruturando o site

- **O que é:** esboço da estrutura das telas, antes do design final
- **Por que usar:** alinhar ideias, validar a estrutura e reduzir retrabalho
- **Tipos:**
  - **Baixa fidelidade:** rascunho simples, foco em estrutura
  - **Alta fidelidade:** próximo do visual final
- **Ferramenta:** [Figma](https://www.figma.com/)

Referência: Diniz et al. (2020).

**Complemento — exemplo de wireframe de baixa fidelidade (homepage):**

```text
+----------------------------------------------------+
| [LOGO]            Início  Sobre  Blog  Contato     |
+----------------------------------------------------+
|                                                    |
|  [ Título principal da empresa ]                   |
|  [ Texto curto de apresentação ]     [  IMAGEM  ]  |
|  [ Botão: Fale conosco ]                           |
|                                                    |
+----------------------------------------------------+
|  [ Produto 1 ]     [ Produto 2 ]     [ Produto 3 ] |
+----------------------------------------------------+
|  Rodapé: contato · redes sociais · endereço        |
+----------------------------------------------------+
```

Repare que não há cores, fontes nem imagens reais: o foco é **onde** cada elemento fica. Na **alta fidelidade**, essa mesma tela ganha cores, tipografia, imagens e comportamento próximo do produto final.

---

## 5. Ferramentas de prototipação

- Prototipação a partir de **imagens e prompts**
- Plugins do Figma: `html.to.design`, `Musho.ai`, entre outros
- Validação de ideias e iterações
- Exemplo prático: exportação de arquivo `.h2d`

---

## 6. Atividade

1. Após definir o tema do projeto do grupo, pesquisar aplicações web similares e identificar **pontos fortes e fracos**.
2. Analisar a estrutura da aplicação: componentes principais, fluxo de navegação e arquitetura.
3. Elaborar **três user stories** (formato "Como... eu quero... para...") e criar **wireframes** das telas principais.
4. Criar conta no **Trello** e montar um quadro **Kanban**, definindo atividades e registrando o que já foi concluído.

---

## Referências

DINIZ, Luciana Mara Freitas et al. Aprendizado Baseado em Projetos em IHC (presencial e remoto): prototipação segundo as heurísticas de Nielsen. In: SIMPÓSIO BRASILEIRO DE FATORES HUMANOS EM SISTEMAS COMPUTACIONAIS (IHC). SBC, 2020. p. 13-18.

GONÇALVES, Rodrigo Franco et al. Uma proposta de processo de produção de aplicações Web. **Production**, v. 15, p. 376-389, 2005.

LUCASSEN, Garm et al. The use and effectiveness of user stories in practice. In: REQUIREMENTS ENGINEERING: FOUNDATION FOR SOFTWARE QUALITY, 22., 2016, Gothenburg. **Proceedings** [...]. Springer International Publishing, 2016. p. 205-222.

SALINAS, C.; SEDEÑO, J.; CUARESMA, M.; RISOTO, M. Agile, Web Engineering and Capability Maturity Model Integration: A systematic literature review. **Information and Software Technology**, v. 71, p. 92-107, 2016. DOI: 10.1016/J.INFSOF.2015.11.002.
