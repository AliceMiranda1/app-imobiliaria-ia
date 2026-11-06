# 🏢 Civitare Imóveis — Plataforma Imobiliária AI-Native & Ecossistema Multiplataforma

[![Google Play Store](https://img.shields.io/badge/Google_Play-App_Publicado-green?style=for-the-badge&logo=googleplay)](https://play.google.com/store)
[![React Native](https://img.shields.io/badge/React_Native-Mobile-blue?style=for-the-badge&logo=react)](https://reactnative.dev/)
[![WordPress REST API](https://img.shields.io/badge/WordPress_API-Backend-blueviolet?style=for-the-badge&logo=wordpress)](https://developer.wordpress.org/rest-api/)
[![AI-Powered](https://img.shields.io/badge/Groq_LLM-Engine-orange?style=for-the-badge&logo=openai)](https://groq.com/)

Plataforma imobiliária completa composta por um **Website Web Responsivo** e um **Aplicativo Mobile (Android em produção na Play Store)**, integrados a um motor de **busca inteligente por linguagem natural (AI-Powered)**. 

O projeto foi concebido e construído sob a metodologia **AI-Native Development**, utilizando modelos generativos avançados (Claude e Gemini) para aceleração de engenharia de software full-stack, design de arquitetura e otimização de APIs.

---

## 📌 Visão Geral do Produto & Arquitetura

A aplicação conecta compradores, inquilinos, corretores e anunciantes em um ecossistema unificado. Os usuários navegam por anúncios moderados, buscam imóveis por conversação com Inteligência Artificial, gerenciam favoritos e solicitam contato direto via WhatsApp.

```
┌────────────────────────────────────────────────────────┐
│               CAMADA DE APRESENTAÇÃO                   │
│   Web (Tema PHP/CSS)     │   Mobile (React Native)     │
└──────────────┬─────────────────────────┬───────────────┘
               │                         │
               └───────────┬─────────────┘
                           ▼
              [ REST API: imobiliaria/v1 ]
                           │
       ┌───────────────────┴───────────────────┐
       ▼                                       ▼
[ WordPress Backend & MySQL ]        [ Groq AI Engine ]
- CPT imovel & lead_imovel           - Function Calling
- Sistema de Recomendação            - Filtros Estruturados
- Autenticação por App Password      - Captura Determinística Lead
```

### 🧱 Arquitetura em Camadas
* **Mobile App:** Desenvolvido em **React Native / Expo (EAS Build)**, com persistência local de sessão, busca conversacional e sincronização em tempo real via API REST.
* **Web & Backend:** **WordPress Headless/Customized** atuando como painel administrativo e servidor de dados.
* **API REST Nativa & Customizada (`imobiliaria/v1`):** Endpoints otimizados para imóveis, autenticação, redefinição segura de senha via OTP (6 dígitos com hash), favoritos e rotas de IA.
* **Autenticação:** Sistema de *Application Passwords* geradas por dispositivo ("App Imobiliária - Data"), garantindo segurança sem exposição de credenciais diretas do MySQL.

---

## 🤖 Inteligência Artificial no Ciclo de Vida e no Produto

É fundamental separar o papel da IA no ciclo de construção do software e na experiência final do produto:

### 1. IA no Ciclo de Desenvolvimento (Engenharia AI-Native)
* **Ferramentas:** Claude (Anthropic) & Gemini (Google).
* **Atuação:** Planejamento arquitetural (definição do fluxo WP REST API + Expo), refatoração full-stack, auditoria de segurança (redesenho do fluxo de senha e captura de formulários), depuração de concorrência e geração acelerada de componentes de interface.

### 2. IA no Produto (Engine Conversacional em Produção)
* **Modelo em Produção:** **Groq LLM** (utilizando a chave em nível de servidor no `wp-config.php`).
* **Busca Híbrida Inteligente:** A IA entende a intenção do usuário via linguagem natural ("*apartamento de 2 quartos com suíte em Poços de Caldas até 400 mil*") e extrai os parâmetros estruturados através de *Function Calling* (`buscar_imoveis`).
* **Execução Segura:** A IA **não inventa dados**. Ela retorna os parâmetros JSON para que a query nativa do WordPress (`imob_query_imoveis_filtrado`) busque os dados reais do MySQL e renderize até 6 cards na tela.
* **Lead Scoring & Conversão:** Captura de contato acionada dinamicamente via backend caso o usuário solicite um corretor ou interaja ativamente na conversa.

---

## 💻 Stack Tecnológica

| Camada | Tecnologias Utilizadas |
| :--- | :--- |
| **Mobile** | React Native, JavaScript, Expo (Snack & EAS Build) |
| **Web & Backend** | WordPress (Tema Personalizado PHP 8+), HTML5, CSS3, JavaScript |
| **Engine de IA** | Groq API (Function Calling + NLP Conversacional) |
| **Banco de Dados** | MySQL (Custom Post Types, Post Meta & User Meta) |
| **Autenticação & E-mail**| Application Passwords, WP Mail SMTP, Brevo API |
| **DevOps & Ferramentas** | VS Code, XAMPP/LAMPP, FileZilla (Deploy FTP), Git/GitHub |

---

## ✨ Funcionalidades Principais

* 🔍 **Busca Conversacional com IA:** Interface de chat no App e na Web alimentada pela Groq LLM.
* 📱 **App Mobile Publicado:** Navegação fluida, modo visitante e perfil de anunciante, busca tolerante a erros de digitação (distância Levenshtein) e notificações *in-app*.
* 🔑 **Autenticação & Segurança:** Registro com validação de DDD/Telefone, login com Application Passwords e redefinição de senha com OTP numérico (30 min de validade).
* 🏢 **Moderação de Anúncios:** Fluxo estrito de aprovação no painel admin para novos imóveis e edições (criação de cópia pendente `_imovel_substituido`).
* 🎯 **Motor de Recomendação:** Sorteio ponderado de imóveis semelhantes baseado no histórico de favoritos, buscas e navegação do usuário.
* ⚖️ **Conformidade LGPD & SEO:** Banner dinâmico de cookies, Schema.org estruturado para imóveis e Open Graph automáticos.

---

## 👩‍💻 Autora

**Alice Miranda** — *Estudante de Ciência da Computação na PUC Minas*  
* Eng. de Software AI-Native & Desenvolvedora Full-Stack / Mobile  
* 🌐 [LinkedIn](https://linkedin.com/in/alicemirandar) | 🐙 [GitHub](https://github.com/AliceMiranda1)
