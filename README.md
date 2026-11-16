# 🏢 Civitare Imóveis — Civitare Imóveis — Ecossistema imobiliário multiplataforma com busca por IA

[![Google Play Store](https://img.shields.io/badge/Google_Play-App_Publicado-green?style=for-the-badge&logo=googleplay)](https://play.google.com/store)
[![React Native](https://img.shields.io/badge/React_Native-Mobile-blue?style=for-the-badge&logo=react)](https://reactnative.dev/)
[![WordPress REST API](https://img.shields.io/badge/WordPress_API-Backend-blueviolet?style=for-the-badge&logo=wordpress)](https://developer.wordpress.org/rest-api/)
[![AI-Powered](https://img.shields.io/badge/Groq_LLM-Engine-orange?style=for-the-badge&logo=openai)](https://groq.com/)

> Projeto desenvolvido em contexto profissional. Este repositório apresenta uma visão geral da solução e das contribuições técnicas, sem disponibilizar o código-fonte ou informações internas protegidas por confidencialidade e propriedade intelectual.

## Visão geral

A **Civitare Imóveis** é um ecossistema digital para o mercado imobiliário, composto por um portal web responsivo e um aplicativo mobile para Android publicado na Google Play Store. As duas interfaces compartilham o mesmo back-end, os dados imobiliários e as regras de negócio.

A plataforma permite consultar imóveis, visualizar detalhes e localização, salvar favoritos, cadastrar anúncios e entrar em contato com a imobiliária. Um dos recursos de destaque é a **busca conversacional com Inteligência Artificial**, que interpreta solicitações em linguagem natural e transforma a intenção do usuário em critérios estruturados de pesquisa.

Os imóveis e demais registros apresentados no ambiente demonstrativo são dados de teste, utilizados para desenvolvimento, validação e apresentação do funcionamento da plataforma.

## Minha atuação

Atuação no desenvolvimento e integração de componentes web, mobile e back-end, incluindo:

- Desenvolvimento da aplicação mobile com React Native e Expo.
- Desenvolvimento e customização do portal e do back-end em WordPress/PHP.
- Implementação e consumo de APIs REST para comunicação entre as interfaces e o servidor.
- Integração da busca conversacional com um modelo de linguagem acessado por meio da Groq API.
- Implementação de fluxos de autenticação, recuperação de senha, favoritos e gerenciamento de anúncios.
- Integração de serviços de e-mail e recursos nativos do dispositivo.

## Arquitetura da solução

A plataforma segue uma arquitetura **cliente-servidor orientada a APIs**. O WordPress customizado atua como back-end central, enquanto o portal web e o aplicativo mobile funcionam como interfaces de acesso.

```text
┌──────────────────────────┐       ┌──────────────────────────┐
│       Portal Web         │       │      App Android         │
│   Tema WordPress/PHP     │       │   React Native + Expo    │
└────────────┬─────────────┘       └────────────┬─────────────┘
             │                                  │
             └──────────────┬───────────────────┘
                            │ HTTP/HTTPS · JSON
                            ▼
              ┌─────────────────────────────┐
              │     Back-end WordPress      │
              │  PHP · APIs REST customizadas│
              └──────────────┬──────────────┘
                             │
                 ┌───────────┴───────────┐
                 ▼                       ▼
       ┌──────────────────┐    ┌────────────────────┐
       │    MySQL         │    │   Serviço de IA    │
       │ Dados imobiliários│    │ Groq API / LLM     │
       └──────────────────┘    └────────────────────┘
```

### Camadas e responsabilidades

- **Aplicativo mobile:** interface Android construída com React Native e Expo, com navegação, busca, favoritos, perfil do usuário, gerenciamento de anúncios, mapas e recursos de dispositivo.
- **Portal web:** interface responsiva construída sobre WordPress, com tema personalizado e componentes em PHP, HTML, CSS e JavaScript.
- **Back-end:** WordPress customizado, responsável pelas regras de negócio, autenticação, gerenciamento dos anúncios e disponibilização de APIs REST.
- **Persistência:** MySQL como fonte central dos dados de usuários, imóveis, metadados, favoritos e status dos anúncios.
- **Integração de IA:** serviço de linguagem acessado pelo back-end por meio da Groq API. A chave de acesso é mantida no ambiente do servidor, não nas interfaces cliente.

## Busca conversacional com IA

A busca inteligente permite que o usuário descreva o imóvel desejado usando linguagem natural, em vez de preencher exclusivamente um conjunto fixo de filtros.

Exemplo de solicitação:

> “Apartamento de dois quartos com suíte em Poços de Caldas até R$ 400 mil.”

O fluxo da busca é organizado da seguinte forma:

1. O usuário envia uma solicitação pela interface web ou mobile.
2. O back-end encaminha o conteúdo ao modelo de linguagem por meio da Groq API.
3. O modelo interpreta a intenção e utiliza **Function Calling** para estruturar os critérios relevantes da busca.
4. O back-end valida e utiliza esses critérios na consulta aos imóveis cadastrados.
5. Os resultados são recuperados da base de dados da plataforma e apresentados ao usuário em cards.

### Separação entre interpretação e recuperação dos dados

A IA é utilizada para interpretar a linguagem natural e estruturar os parâmetros da pesquisa. A recuperação dos imóveis é executada pelo back-end sobre os registros existentes na plataforma.

Essa separação reduz o risco de apresentar como reais imóveis ou características que não estejam cadastrados: o modelo não é a fonte de verdade dos anúncios. Os dados exibidos vêm da base da aplicação.

A implementação contempla a apresentação de até seis resultados por consulta, conforme os critérios e a disponibilidade de registros compatíveis.

## IA no ciclo de desenvolvimento

Além da IA integrada ao produto, ferramentas generativas foram utilizadas como apoio ao processo de engenharia:

- **Claude e Gemini:** apoio ao planejamento técnico, exploração de soluções, refatoração, depuração e revisão de componentes.
- **Groq API:** integração de inferência de modelo de linguagem à funcionalidade de busca conversacional do produto.

Esses papéis são distintos: Claude e Gemini foram utilizados como ferramentas de apoio ao desenvolvimento; a busca disponibilizada ao usuário utiliza o serviço de inferência integrado por meio da Groq API.

## Funcionalidades implementadas

### Experiência de busca e descoberta

- Busca de imóveis por critérios e por linguagem natural.
- Exibição de imóveis em listas e cards.
- Visualização de localização por recursos de mapas.
- Busca com tolerância a erros de digitação, utilizando distância de Levenshtein.
- Motor de recomendação que realiza seleção ponderada de imóveis semelhantes, considerando sinais de interação descritos na aplicação, como favoritos, buscas e navegação.

### Contas e interação do usuário

- Cadastro, login e gerenciamento de perfil.
- Favoritos associados à conta do usuário e sincronizados pelo servidor, com atualização otimista da interface durante a requisição.
- Solicitação de contato com a imobiliária e captação contextual de leads quando há intenção de falar com um corretor ou avançar no atendimento.
- Notificações in-app para eventos e interações da aplicação.
- Recuperação de senha por código temporário de seis dígitos, armazenado de forma protegida por hash e com validade de 30 minutos.

### Publicação e moderação de anúncios

- Cadastro e edição de anúncios pelo usuário.
- Fluxo de revisão e aprovação administrativa.
- Estados de publicação para distinguir anúncios pendentes e publicados.
- Tratamento de alterações de anúncios por meio de revisão antes da substituição da versão publicada, conforme as regras da plataforma.

### Recursos complementares

- Integração com WhatsApp para contato.
- Envio de e-mails transacionais por integração de SMTP/serviço de e-mail.
- Geolocalização e seleção de imagens no aplicativo.
- Recursos de SEO, dados estruturados para páginas de imóveis e metadados para compartilhamento.
- Interface de consentimento de cookies.

## Stack tecnológica

| Camada | Tecnologias |
|---|---|
| Aplicativo mobile | JavaScript, React Native, Expo, EAS Build |
| Web e back-end | WordPress, PHP 8+, HTML5, CSS3, JavaScript |
| Integração | APIs REST, HTTP/HTTPS, JSON |
| Inteligência Artificial | Groq API, LLM, Function Calling |
| Banco de dados | MySQL |
| Autenticação e e-mail | WordPress Application Passwords, fluxo de código temporário, WP Mail SMTP, Brevo |
| Desenvolvimento | VS Code, XAMPP/LAMPP, Git, GitHub |

## Decisões e aspectos de engenharia

- **Back-end centralizado:** web e mobile utilizam a mesma fonte de dados e regras de negócio, evitando manter bases independentes para cada interface.
- **Integração por API:** a comunicação entre clientes e servidor ocorre por requisições HTTP/HTTPS com payloads JSON.
- **Separação de responsabilidades na busca por IA:** o LLM interpreta a solicitação; o back-end valida os parâmetros e consulta a fonte de dados.
- **Credenciais no servidor:** a integração com o provedor de IA é realizada pelo back-end, evitando expor a chave da API no aplicativo ou no navegador.
- **Autenticação por dispositivo:** o aplicativo utiliza Application Passwords gerenciadas por dispositivo pelo back-end, em vez de acessar diretamente o banco de dados.

## Confidencialidade

A Civitare Imóveis foi desenvolvida em contexto profissional e pertence ao ambiente de trabalho da empresa. Por esse motivo, o código-fonte, credenciais, configurações privadas, dados de usuários, registros imobiliários reais e detalhes internos de implementação não são publicados neste repositório.

Este README descreve a arquitetura em nível conceitual, as tecnologias e as funcionalidades relevantes para demonstrar a experiência técnica, respeitando os limites de divulgação e a propriedade intelectual do projeto.

---
## 👩‍💻 Autora

**Alice Miranda** — *Estudante de Ciência da Computação na PUC Minas*    
* 🌐 [LinkedIn](https://linkedin.com/in/alicemirandar) | 🐙 [GitHub](https://github.com/AliceMiranda1)
---
*Nota: este repositório é uma documentação de portfólio. Não contém o código-fonte da plataforma nem disponibiliza acesso ao ambiente interno da empresa.*
