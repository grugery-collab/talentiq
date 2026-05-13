# TalentIQ — Plataforma de Recrutamento com IA

Plataforma completa de recrutamento com IA integrada via Anthropic Claude.

## Funcionalidades

- **Projetos** — crie múltiplos projetos de recrutamento
- **Análise de JD** — IA analisa o Job Description e extrai competências, perfil ideal, red flags
- **Mercado** — notícias e tendências do segmento geradas por IA
- **Empresas** — mapeamento de concorrentes e empresas similares
- **Candidatos** — análise de CV vs JD com score de compatibilidade
- **Entrevistas** — anotações + geração de parecer formal com IA
- **Status** — aprovado / em análise / reprovado por candidato

---

## Deploy no Netlify (passo a passo)

### 1. Pré-requisitos

- Conta no [Netlify](https://netlify.com) (gratuita)
- Conta na [Anthropic](https://console.anthropic.com) com API Key
- [Node.js](https://nodejs.org) instalado (v18+)
- [Git](https://git-scm.com) instalado

---

### 2. Estrutura do projeto

```
talentiq/
├── netlify.toml                  ← configuração do Netlify
├── public/
│   └── index.html                ← frontend completo
└── netlify/
    └── functions/
        └── claude.js             ← função serverless (proxy da API)
```

---

### 3. Subir para o GitHub

```bash
cd talentiq
git init
git add .
git commit -m "TalentIQ inicial"
```

Crie um repositório no GitHub e conecte:

```bash
git remote add origin https://github.com/SEU_USUARIO/talentiq.git
git push -u origin main
```

---

### 4. Deploy no Netlify

1. Acesse [app.netlify.com](https://app.netlify.com)
2. Clique em **"Add new site" → "Import an existing project"**
3. Escolha **GitHub** e selecione o repositório `talentiq`
4. Configurações de build:
   - **Build command:** *(deixe em branco)*
   - **Publish directory:** `public`
5. Clique em **"Deploy site"**

---

### 5. Configurar a API Key da Anthropic

> ⚠️ Este passo é obrigatório — sem ele a IA não funciona.

1. No painel do Netlify, vá em **Site configuration → Environment variables**
2. Clique em **"Add a variable"**
3. Adicione:
   - **Key:** `ANTHROPIC_API_KEY`
   - **Value:** `sk-ant-...` *(sua chave da Anthropic)*
4. Clique em **"Save"**
5. Vá em **Deploys → Trigger deploy → Deploy site** para aplicar

---

### 6. Acessar o app

Após o deploy, o Netlify fornece uma URL como:
```
https://talentiq-XXXXX.netlify.app
```

Você pode configurar um domínio personalizado nas configurações do site.

---

## Como usar

### Criando um projeto
1. Clique em **"Novo projeto"** na sidebar
2. Dê um nome e informe o cargo principal

### Analisando uma vaga
1. Selecione o projeto
2. Cole o JD na aba **Vaga**
3. Clique em **"Analisar com IA"**

### Pesquisando o mercado
1. Aba **Mercado** → digite o segmento ou clique em **"Do JD"**
2. Aba **Empresas** → mapeie concorrentes automaticamente

### Avaliando candidatos
1. Aba **Candidatos** → clique em **"Adicionar candidato"**
2. Cole o CV e clique **"Analisar compatibilidade"** (recebe um score de 0–100)
3. Anote observações da entrevista
4. Clique **"Gerar parecer"** para o relatório formal de RH
5. Defina o status: Aprovado / Em análise / Reprovado

---

## Tecnologias

- **Frontend:** HTML5 + CSS3 + JavaScript vanilla
- **Backend:** Netlify Functions (Node.js serverless)
- **IA:** Anthropic Claude claude-sonnet-4-20250514
- **Dados:** localStorage (persistência local no navegador)
- **Deploy:** Netlify CDN

---

## Segurança

A API Key da Anthropic **nunca fica exposta no frontend**. Toda comunicação com a API passa pela função serverless `/api/claude`, que lê a chave das variáveis de ambiente do Netlify.

---

## Custos estimados

| Item | Custo |
|------|-------|
| Netlify (plano gratuito) | $0/mês |
| Anthropic API (uso moderado) | ~$2–10/mês |

O plano gratuito do Netlify inclui 125k invocações de function/mês — suficiente para uso profissional individual.
