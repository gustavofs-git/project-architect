# Project Architect Setup - Framework de Desenvolvimento Assistido por IA

## Sobre Este Repositório

Este repositório é baseado no trabalho original de Rasmus Widing: https://github.com/Wirasm/PRPs-agentic-eng

Framework completo para desenvolvimento assistido por IA que gera arquitetura completa de projetos, incluindo planejamento, configuração e PRPs individuais para cada feature.

## Como Funciona

### 🎯 Fluxo Completo: Da Ideia ao Código

**1. Você descreve seu projeto:**
```
/setup-project-claude portifolio com hero, about me, contact form, serviços, projetos do YouTube, suporte PT-BR/EN
```

**2. O sistema gera tudo automaticamente:**
- ✅ **Arquivos CLAUDE.md** customizados (frontend + backend)
- ✅ **Planning completo** do projeto com arquitetura  
- ✅ **PRPs individuais** para cada feature (hero, contact, etc.)
- ✅ **Comando de execução** para rodar todos os PRPs

**3. Você executa tudo em sequência:**
```
/execute-all-prps portfolio
```

## Exemplo Prático

### Input:
```
/setup-project-claude ecommerce com produtos, carrinho, checkout, pagamentos Stripe, admin panel, usando React e Python
```

### Output Automático:
```
📁 Estrutura Criada:
├── CLAUDE.md                    # Orquestrador geral
├── frontend/CLAUDE.md           # React + Tailwind
├── backend/CLAUDE.md            # Python + FastAPI  
└── PRPs/
    ├── ecommerce-planning.md    # Planning geral
    ├── ecommerce-products.md    # Catálogo de produtos
    ├── ecommerce-cart.md        # Sistema de carrinho
    ├── ecommerce-checkout.md    # Processo de checkout
    ├── ecommerce-payments.md    # Integração Stripe
    ├── ecommerce-admin.md       # Painel administrativo
    ├── ecommerce-database.md    # Setup do banco
    ├── ecommerce-api.md         # APIs backend
    └── ecommerce-deployment.md  # Deploy produção

⚡ Comando criado: /execute-all-prps ecommerce
```

## Comandos Principais

### 🏗️ Geração Completa de Projeto
```bash
/setup-project-claude [descrição do projeto]
```
**O que faz:**
- Faz perguntas para completar entendimento
- Gera CLAUDE.md para tecnologias detectadas
- Cria planning detalhado do projeto
- Quebra projeto em PRPs individuais
- Cria comando de execução personalizado

### 🚀 Execução Automática
```bash
/execute-all-prps [nome-do-projeto]
```
**O que faz:**
- Lista todos PRPs do projeto
- Executa em ordem lógica (database → backend → frontend → deployment)
- Tracking de progresso em tempo real
- Handling de erros com opções de recovery
- Relatório final completo

### 📋 Comandos de Criação Individual
- `/prp-base-create [feature]` - Cria PRP específico
- `/prp-planning-create [projeto]` - Só o planning
- `/prp-task-create [tarefa]` - Task pontual

### ⚙️ Utilitários
- `/prime-core` - Contextualiza Claude com projeto
- `/smart-commit` - Commit inteligente
- `/review-staged-unstaged` - Review antes do commit

## Modos de Execução

### 🤖 Automático (Headless)
```bash
/execute-all-prps portfolio
# Escolhe modo [A] - Executa tudo automaticamente
```

### 👤 Passo-a-Passo (Interativo)
```bash
/execute-all-prps portfolio  
# Escolhe modo [S] - Pausa entre cada PRP
```

### 🎯 Seleção Customizada
```bash
/execute-all-prps portfolio
# Escolhe modo [C] - Seleciona PRPs específicos (ex: 1 3 5-7)
```

## Tipos de Projetos Suportados

### 🌐 Websites/Portfolios
```bash
/setup-project-claude portfolio com hero, about, contact, projects, blog
```

### 🛒 E-commerce
```bash
/setup-project-claude loja online com produtos, carrinho, pagamentos, admin
```

### 📱 Apps Mobile
```bash
/setup-project-claude app fitness tracker com exercícios, progresso, social
```

### 💼 SaaS/Dashboards
```bash
/setup-project-claude SaaS analytics com auth, dashboards, billing, APIs
```

### 📝 Blogs/CMS
```bash
/setup-project-claude blog pessoal com posts, comments, newsletter, SEO
```

## Fluxo de Perguntas Automáticas

O sistema faz perguntas inteligentes para completar o entendimento:

```
🤔 Perguntas Típicas:
- "Que tecnologias prefere? React/Vue/Next.js para frontend?"
- "Backend em Python/Node.js/PHP?"
- "Precisa de banco de dados? PostgreSQL/MongoDB?"
- "Onde vai hospedar? Vercel/AWS/Netlify?"
- "Precisa de autenticação de usuários?"
- "Algum design system específico?"
- "Qual a complexidade desejada? Simples/Média/Avançada?"
```

## Exemplos de Estruturas Geradas

### Para Projetos Fullstack:
```
projeto/
├── CLAUDE.md              # Orquestrador geral
├── frontend/
│   ├── CLAUDE.md          # React/Vue específico
│   └── src/
├── backend/
│   ├── CLAUDE.md          # Python/Node específico
│   └── src/
└── PRPs/
    ├── [projeto]-planning.md
    ├── [projeto]-database.md
    ├── [projeto]-api.md
    ├── [projeto]-[feature1].md
    ├── [projeto]-[feature2].md
    └── [projeto]-deployment.md
```

### Para Mobile Apps:
```
app/
├── CLAUDE.md              # Flutter/React Native
├── lib/                   # Source code
└── PRPs/
    ├── app-planning.md
    ├── app-navigation.md
    ├── app-features.md
    └── app-deployment.md
```

## Exemplo Real de Uso

Work in progress



## Instalação e Setup

```bash
# Clone este repositório
git clone https://github.com/seu-usuario/project-architect-setup.git
cd project-architect-setup

# Para usar em projeto existente:
cp -r .claude/commands /seu-projeto/.claude/
cp -r PRPs /seu-projeto/

# Ou use este repo diretamente
```


## Licença

MIT License

## Referência Original

- **Repositório Original**: https://github.com/Wirasm/PRPs-agentic-eng
- **Autor**: Rasmus Widing  
- **Website**: https://www.rasmuswiding.com/
