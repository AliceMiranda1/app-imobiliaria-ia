# Civitare Imóveis: ecossistema imobiliário multiplataforma com busca por IA

[![Google Play](https://img.shields.io/badge/Google_Play-Publicado-green?style=for-the-badge&logo=googleplay)](https://play.google.com/store)
[![React Native](https://img.shields.io/badge/React_Native-Mobile-blue?style=for-the-badge&logo=react)](https://reactnative.dev/)
[![WordPress](https://img.shields.io/badge/WordPress-Backend-blueviolet?style=for-the-badge&logo=wordpress)](https://wordpress.org/)
[![AI](https://img.shields.io/badge/IA-Busca_conversacional-orange?style=for-the-badge)](https://groq.com/)

> **Aviso de confidencialidade:** este projeto foi desenvolvido em contexto profissional. Este repositório apresenta apenas uma visão geral da solução e das contribuições técnicas. Não contém código-fonte, credenciais, configurações privadas, dados de usuários ou registros reais de imóveis.

## Visão geral

A Civitare Imóveis é um ecossistema digital para o mercado imobiliário, com um portal web responsivo e um aplicativo Android publicado na Google Play Store. As duas interfaces compartilham o mesmo back-end, os mesmos dados e as mesmas regras de negócio.

Os usuários consultam imóveis, visualizam detalhes e localização, salvam favoritos, cadastram anúncios e entram em contato com a imobiliária. O destaque é a **busca conversacional com IA**, que transforma uma descrição em linguagem natural em critérios estruturados de pesquisa.

Os imóveis exibidos no ambiente de testes são dados fictícios, usados para desenvolvimento, validação e demonstração do funcionamento da plataforma.

#### Link do Site: [civitare.ia.br](https://civitare.ia.br)

## Minha atuação

- Desenvolvimento do aplicativo mobile com React Native e Expo.
- Desenvolvimento e customização do portal e do back-end em WordPress e PHP.
- Implementação e consumo de APIs REST para comunicação entre as interfaces e o servidor.
- Integração da busca conversacional com um modelo de linguagem acessado pela Groq API.
- Implementação de autenticação, recuperação de senha, favoritos e gerenciamento de anúncios.
- Integração de serviços de e-mail e de recursos nativos do dispositivo.

## Arquitetura

A plataforma segue uma arquitetura cliente-servidor orientada a APIs. O back-end centraliza as regras de negócio e os dados, e o portal web e o aplicativo mobile funcionam como interfaces de acesso.

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
              │      APIs REST              │
              └──────────────┬──────────────┘
                             │
                 ┌───────────┴───────────┐
                 ▼                       ▼
       ┌──────────────────┐    ┌────────────────────┐
       │    MySQL         │    │   Serviço de IA    │
       │ Dados da plataforma│  │ Groq API / LLM     │
       └──────────────────┘    └────────────────────┘
```

## Busca conversacional com IA

O usuário descreve o imóvel que procura em linguagem natural, em vez de preencher apenas filtros fixos.

> "Apartamento de dois quartos com suíte em Poços de Caldas até R$ 400 mil."

1. O usuário envia a solicitação pela interface web ou mobile.
2. O back-end encaminha o texto ao modelo de linguagem.
3. O modelo interpreta a intenção e estrutura os critérios da busca por meio de Function Calling.
4. O back-end valida esses critérios e consulta os imóveis cadastrados na plataforma.
5. Os resultados são exibidos ao usuário em cards.

**Separação entre interpretação e dados:** a IA interpreta a linguagem natural e estrutura os parâmetros. A recuperação dos imóveis é feita pelo back-end, sobre os registros da própria plataforma. O modelo não é a fonte dos anúncios, o que reduz o risco de apresentar imóveis ou características que não estejam cadastrados.

## Uso de IA no desenvolvimento

Além da IA integrada ao produto, ferramentas generativas (Claude e Gemini) foram usadas como apoio ao planejamento técnico, à exploração de soluções, à refatoração, à depuração e à revisão de componentes. A busca oferecida ao usuário é um recurso separado, atendido pela Groq API.

## Funcionalidades

**Busca e descoberta**
- Busca por critérios e por linguagem natural, com resultados em listas e cards.
- Visualização de localização em mapa.
- Busca com tolerância a erros de digitação.
- Recomendação de imóveis semelhantes a partir das interações do usuário.

**Contas e interação**
- Cadastro, login e gerenciamento de perfil.
- Favoritos associados à conta, sincronizados com o servidor.
- Solicitação de contato com a imobiliária.
- Notificações dentro do aplicativo.
- Recuperação de senha por código temporário.

**Anúncios**
- Cadastro e edição de anúncios pelo usuário.
- Fluxo de revisão e aprovação antes da publicação.
- Estados distintos para anúncios pendentes e publicados.

**Recursos complementares**
- Contato direto por WhatsApp.
- E-mails transacionais.
- Recursos de SEO e metadados para compartilhamento.
- Aviso de cookies em conformidade com a LGPD.

## Stack tecnológica

| Camada | Tecnologias |
|---|---|
| Aplicativo mobile | JavaScript, React Native, Expo |
| Web e back-end | WordPress, PHP, HTML5, CSS3, JavaScript |
| Integração | APIs REST, HTTP/HTTPS, JSON |
| Inteligência Artificial | Groq API, LLM, Function Calling |
| Banco de dados | MySQL |
| Autenticação e e-mail | Serviços de autenticação e envio de mensagens transacionais |
| Ferramentas | Git, GitHub |

## Autora

**Alice Miranda**, estudante de Ciência da Computação na PUC Minas
[LinkedIn](https://linkedin.com/in/alicemirandar) · [GitHub](https://github.com/AliceMiranda1)
