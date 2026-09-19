# Aula 04 — Servidores e opções de hospedagem / CMS

> Prof. Me. Deivison S. Takatu

## Sumário

1. [Registro de domínio](#1-registro-de-domínio)
2. [Hospedagem de sites](#2-hospedagem-de-sites)
3. [CMS](#3-sistema-de-gerenciamento-de-conteúdo-cms)
4. [WordPress](#4-wordpress)
5. [Atividade](#5-atividade)
6. [Referências](#referências)

---

## 1. Registro de domínio

**Domínio:** endereço único do site (ex.: `www.meusite.com`).

**Onde registrar:**

- **Diretamente:** Registro.br, GoDaddy, Namecheap
- **Via hospedagem:** HostGator, Hostinger, Locaweb (domínio grátis no plano anual)
- **Marketplaces:** domínios premium já registrados (Sedo, Flippa)

**Boas práticas:**

- Nome **curto, memorável**, fácil de escrever e relacionado ao projeto; evitar números e hífens
- Extensões comuns: `.com` (popular e confiável), `.org` (ideal para ONGs)
- Verificar disponibilidade em registradores confiáveis e evitar marcas registradas
- Registrar variantes, para proteger a marca e evitar erros de digitação

---

## 2. Hospedagem de sites

Serviço que mantém o site em um servidor acessível na internet. Exemplos de empresas: HostGator, Hostinger e Locaweb.

**Complemento — principais tipos de hospedagem:**

| Tipo | Como funciona | Indicado para |
|---|---|---|
| Compartilhada | Vários sites no mesmo servidor; barata, recursos limitados | Blogs e sites pequenos |
| VPS | Parte isolada de um servidor, com recursos reservados e mais controle | Projetos médios |
| Dedicada | Servidor inteiro só para você | Alto tráfego ou exigências específicas |
| Cloud | Recursos escaláveis sob demanda | Aplicações que crescem ou variam de uso |
| Estática | Só arquivos prontos (HTML, CSS, JS), com deploy via Git (ex.: Vercel) | Sites estáticos e SPAs |

**Como domínio e hospedagem se conectam:** o domínio é o "nome", e a hospedagem é o "lugar" onde o site mora. O **DNS** faz a ligação, apontando o domínio para o servidor da hospedagem. Isso é configurado no painel do registrador ou da hospedagem.

---

## 3. Sistema de Gerenciamento de Conteúdo (CMS)

Plataforma para **criar, modificar e publicar** conteúdo digital, com colaboração entre vários usuários e diferentes níveis de permissão.

**Principais funcionalidades:**

- **Gerenciamento de conteúdo:** texto, formatação, vídeos, fotos, áudio e código
- **SEO integrado:** URLs amigáveis
- **Suporte e comunidade:** suporte online e comunidades ativas
- **Gestão de usuários:** funções por usuário e grupo
- **Design flexível:** templates e designs personalizados

Estatísticas de uso de CMS: [W3Techs](https://w3techs.com/).

---

## 4. WordPress

CMS de **código aberto** (download e personalização gratuitos), um dos mais populares do mundo. Serve para blogs, sites corporativos, lojas virtuais e mais.

**Vantagens:**

- Fácil de usar, com interface intuitiva
- Extensível: milhares de plugins e temas
- Comunidade ativa e atualizações constantes

### WordPress.com x WordPress.org

| WordPress.com | WordPress.org |
|---|---|
| Plataforma gratuita para criar e hospedar blogs | Software gratuito para baixar e instalar |
| Não exige hospedagem nem domínio próprio | Exige hospedagem própria e registro de domínio |
| Domínio limitado a `seusite.wordpress.com` | Domínio próprio (ex.: `seusite.com.br`) |
| Menos flexibilidade | Maior controle (temas, plugins, funcionalidades) |
| — | Exige conhecimento técnico |

Referências: MacDonald (2020); Coleman (2019).

### Possibilidades

Blogs pessoais e profissionais, sites corporativos e institucionais, portais de notícias, e-commerce, aplicativos mobile, gerenciadores de projetos, redes sociais, sistemas de ensino e treinamento.

Exemplos de uso: USP, Casa Branca (whitehouse.gov) e a [vitrine do WordPress](https://wordpress.org/showcase/).

### Instalando o WordPress (visão geral)

**Complemento:** passos típicos do WordPress.org.

1. Contratar uma **hospedagem** e registrar (ou apontar) o **domínio**
2. Instalar o WordPress: a maioria das hospedagens tem instalador de 1 clique
3. Acessar o painel em `seusite.com/wp-admin` com o usuário e a senha criados
4. Escolher e ativar um **tema** (*Aparência → Temas*)
5. Instalar os **plugins** necessários (*Plugins → Adicionar novo*)
6. Editar a página inicial e criar páginas e posts

### Temas

- A "casca" do site: define **layout e design**
- Compostos por imagens, scripts (PHP e JavaScript) e folhas de estilo (CSS)
- Permitem integração com plugins e ferramentas externas
- Podem ser gratuitos ou pagos
- Recomenda-se criar ou personalizar um tema conforme as necessidades do projeto

### Plugins

- Complementos que **agregam ou modificam funcionalidades**
- Vão de funções simples a integrações complexas (e-commerce, SEO, segurança etc.)
- Lista dos mais populares: [br.wordpress.org/plugins](https://br.wordpress.org/plugins/browse/popular/)

### Páginas e widgets

- **Páginas:** características gerais dos posts, com recursos extras (hierarquia, templates e outros atributos)
- **Widgets:** pequenas caixas de conteúdo, dinâmicas ou estáticas, exibidas em áreas específicas (lista de links, arquivos, categorias etc.)

**Complemento — post x página:**

| | Post | Página |
|---|---|---|
| Conteúdo | Cronológico (novidades, artigos) | Estático (Sobre, Contato) |
| Organização | Categorias e tags | Hierarquia (página pai e filhas) |
| Aparece no blog | Sim | Não |

---

## 5. Atividade

1. Criar conta em uma ferramenta de hospedagem (sugestão gratuita: [Pantheon](https://pantheon.io/)), configurar o ambiente, instalar um CMS e testar o acesso e as funcionalidades essenciais.
2. Personalizar com **temas e plugins**, editar a página inicial (layout, textos, elementos visuais) e compilar todo o processo em um documento, submetendo o arquivo no repositório do GitHub.

---

## Referências

MACDONALD, Matthew. **WordPress**: The Missing Manual. 3. ed. Sebastopol: O'Reilly Media, 2020. ISBN 978-1492074167.

MESSENLEHNER, Brian; COLEMAN, Jason. **Building Web Apps with WordPress**: WordPress as an Application Framework. 2. ed. Sebastopol: O'Reilly Media, 2019. ISBN 978-1491990048.

PANTHEON. **WebOps Platform for Drupal & WordPress Hosting**. Disponível em: https://pantheon.io/.

W3TECHS. **Usage statistics and market share of content management systems**. Disponível em: https://w3techs.com/.

WORDPRESS. **WordPress – Crie um site ou blog gratuitamente**. Disponível em: https://wordpress.org/.
