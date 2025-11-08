# FinancialDash 📊

Dashboard financeiro interativo com análise de volatilidade, modelos de Markov ocultos e visualização de dados de mercado.

> **Nota:** Este projeto foi consolidado a partir de dois repositórios separados que foram desenvolvidos inicialmente de forma independente:
> - **Backend**: [BackendAlphaTrading](https://github.com/thales700/BackendAlphaTrading)
> - **Frontend**: [FrontendAlphaTrading](https://github.com/thales700/FrontendAlphaTrading)

## 📋 Índice

- [Sobre o Projeto](#sobre-o-projeto)
- [Tecnologias Utilizadas](#tecnologias-utilizadas)
- [Pré-requisitos](#pré-requisitos)
- [Instalação e Execução](#instalação-e-execução)
  - [Opção 1: Com Docker (Recomendado)](#opção-1-com-docker-recomendado)
  - [Opção 2: Sem Docker](#opção-2-sem-docker)
- [Estrutura do Projeto](#estrutura-do-projeto)
- [API Endpoints](#api-endpoints)
- [Funcionalidades](#funcionalidades)
- [Desenvolvimento](#desenvolvimento)
- [Licença](#licença)

## 🎯 Sobre o Projeto

FinancialDash é uma aplicação web completa para análise financeira que combina:

- **Backend FastAPI**: API REST para processamento de dados financeiros
- **Frontend React**: Interface interativa com gráficos e visualizações
- **Análise de Volatilidade**: Modelos GARCH para análise de volatilidade
- **Modelos de Markov**: Identificação de regimes de mercado usando HMM (Hidden Markov Models)
- **Dados de Mercado**: Integração com dados de cotações e símbolos financeiros

## 🚀 Tecnologias Utilizadas

### Backend
- **Python 3.12**
- **FastAPI**: Framework web moderno e rápido
- **yfinance**: Coleta de dados financeiros do Yahoo Finance
- **pandas & numpy**: Manipulação e análise de dados
- **hmmlearn**: Implementação de Hidden Markov Models
- **arch**: Modelos ARCH/GARCH para volatilidade

### Frontend
- **React 19**: Biblioteca JavaScript para interfaces
- **TypeScript**: Superset tipado do JavaScript
- **Vite**: Build tool e dev server
- **TailwindCSS**: Framework CSS utilitário
- **Recharts & ApexCharts**: Bibliotecas de gráficos
- **Radix UI**: Componentes acessíveis
- **React Router**: Roteamento no frontend

### DevOps
- **Docker**: Containerização
- **Docker Compose**: Orquestração de containers

## 📦 Pré-requisitos

### Para executar com Docker (Recomendado):
- [Docker](https://www.docker.com/get-started) (versão 20.10 ou superior)
- [Docker Compose](https://docs.docker.com/compose/install/) (versão 1.29 ou superior)

### Para executar sem Docker:
- [Python 3.12+](https://www.python.org/downloads/)
- [Node.js 20+](https://nodejs.org/) e npm
- [Git](https://git-scm.com/)

## 🔧 Instalação e Execução

### Opção 1: Com Docker (Recomendado)

Esta é a forma mais simples e consistente de executar o projeto.

#### 1. Clone o repositório

```bash
git clone <url-do-repositorio>
cd FinancialDash
```

#### 2. Execute com Docker Compose

```bash
docker-compose up --build
```

Este comando irá:
- Construir as imagens do backend e frontend
- Instalar todas as dependências
- Iniciar os serviços

#### 3. Acesse a aplicação

- **Frontend**: http://localhost:5173
- **Backend API**: http://localhost:8000
- **Documentação API (Swagger)**: http://localhost:8000/docs

#### Comandos úteis do Docker

```bash
# Parar os containers
docker-compose down

# Parar e remover volumes
docker-compose down -v

# Ver logs do backend
docker-compose logs -f backend

# Ver logs do frontend
docker-compose logs -f frontend

# Reconstruir apenas um serviço
docker-compose up --build backend
docker-compose up --build frontend

# Executar comandos dentro do container
docker-compose exec backend bash
docker-compose exec frontend sh
```

### Opção 2: Sem Docker

#### Backend

1. **Navegue até a pasta do backend**

```bash
cd backend
```

2. **Crie um ambiente virtual Python** (recomendado)

```bash
# Windows
python -m venv venv
venv\Scripts\activate

# Linux/Mac
python3 -m venv venv
source venv/bin/activate
```

3. **Instale as dependências**

```bash
pip install --upgrade pip
pip install -r requirements.txt
```

4. **Execute o servidor FastAPI**

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

O backend estará disponível em:
- API: http://localhost:8000
- Documentação interativa: http://localhost:8000/docs

#### Frontend

1. **Abra um novo terminal e navegue até a pasta do frontend**

```bash
cd frontend
```

2. **Instale as dependências**

```bash
npm install
```

3. **Configure a variável de ambiente** (opcional)

Crie um arquivo `.env` na pasta `frontend`:

```env
VITE_API_URL=http://localhost:8000
```

4. **Execute o servidor de desenvolvimento**

```bash
npm run dev
```

O frontend estará disponível em: http://localhost:5173

## 📁 Estrutura do Projeto

```
FinancialDash/
│
├── backend/                    # Backend FastAPI
│   ├── API/                    # Rotas da API
│   │   └── routers/
│   │       ├── symbol_data.py        # Endpoints de dados de símbolos
│   │       ├── symbol_hmm.py         # Endpoints de Markov
│   │       └── symbol_volatility.py  # Endpoints de volatilidade
│   ├── entities/               # Entidades e modelos de domínio
│   │   ├── ArchModels.py
│   │   ├── Distribution.py
│   │   ├── Granularity.py
│   │   └── Symbols.py
│   ├── schemas/                # Schemas Pydantic
│   │   └── symbol_properties.py
│   ├── services/               # Lógica de negócio
│   │   ├── GarchLevels.py
│   │   ├── HiddenMarkovModel.py
│   │   └── Quotations.py
│   ├── mock_data/              # Dados mockados para testes
│   ├── tests/                  # Testes da aplicação
│   ├── main.py                 # Ponto de entrada da API
│   ├── requirements.txt        # Dependências Python
│   └── Dockerfile
│
├── frontend/                   # Frontend React
│   ├── src/
│   │   ├── components/         # Componentes reutilizáveis
│   │   │   ├── ui/             # Componentes UI base
│   │   │   ├── dashboard-grid.tsx
│   │   │   ├── layout.tsx
│   │   │   └── ...
│   │   ├── pages/              # Páginas da aplicação
│   │   │   ├── dashboard/      # Dashboard principal
│   │   │   ├── assets/         # Página de ativos
│   │   │   ├── markov-chains/  # Página de Markov
│   │   │   └── volatility/     # Página de volatilidade
│   │   ├── hooks/              # Custom hooks
│   │   ├── lib/                # Utilitários
│   │   ├── mock/               # Dados mockados
│   │   └── main.tsx            # Ponto de entrada
│   ├── package.json            # Dependências Node.js
│   ├── vite.config.ts          # Configuração do Vite
│   └── Dockerfile
│
└── docker-compose.yml          # Orquestração Docker

```

## 🔌 API Endpoints

### Dados de Símbolos
- `GET /symbols/quotations` - Obter cotações de símbolos
- Outros endpoints relacionados a dados de mercado

### Hidden Markov Model (HMM)
- Endpoints para análise de regimes de mercado usando modelos de Markov

### Volatilidade
- Endpoints para análise de volatilidade usando modelos GARCH

Acesse http://localhost:8000/docs para documentação completa e interativa da API.

## ✨ Funcionalidades

### Dashboard Principal
- Visão geral dos principais indicadores financeiros
- Gráficos interativos e customizáveis
- Layout responsivo e adaptável

### Análise de Ativos
- Visualização de cotações históricas
- Gráficos de candlestick interativos
- Análise de múltiplos símbolos

### Modelos de Markov
- Identificação de regimes de mercado
- Visualização de estados ocultos
- Probabilidades de transição

### Análise de Volatilidade
- Modelos GARCH para previsão de volatilidade
- Visualização de níveis de volatilidade
- Análise histórica e previsões

## 🛠️ Desenvolvimento

### Estrutura de Desenvolvimento

#### Backend

```bash
cd backend

# Ativar ambiente virtual
source venv/bin/activate  # Linux/Mac
venv\Scripts\activate     # Windows

# Instalar dependências de desenvolvimento
pip install -r requirements.txt

# Executar testes
python -m pytest tests/

# Gerar dados mockados
python GenerateMockData.py
```

#### Frontend

```bash
cd frontend

# Instalar dependências
npm install

# Modo de desenvolvimento
npm run dev

# Build de produção
npm run build

# Preview do build
npm run preview

# Linting
npm run lint
```

### Boas Práticas

1. **Backend**
   - Use type hints em Python
   - Documente funções com docstrings
   - Siga PEP 8 para estilo de código
   - Crie testes para novas funcionalidades

2. **Frontend**
   - Use TypeScript para type safety
   - Componentes devem ser reutilizáveis
   - Siga as convenções do React
   - Mantenha os componentes pequenos e focados

### Gerando Dados Mockados

O projeto inclui um gerador de dados mockados para desenvolvimento:

```bash
cd backend
python GenerateMockData.py
```

Isso irá gerar arquivos JSON em `backend/mock_data/` com dados simulados.

## 📝 Scripts Disponíveis

### Backend
```bash
# Executar servidor em modo desenvolvimento
uvicorn main:app --reload

# Executar em uma porta específica
uvicorn main:app --reload --port 8080

# Executar testes
python -m pytest
```

### Frontend
```bash
# Desenvolvimento
npm run dev

# Build
npm run build

# Preview
npm run preview

# Lint
npm run lint
```

## 🐛 Troubleshooting

### Problemas Comuns

#### Docker não inicia
```bash
# Verificar se o Docker está rodando
docker --version
docker-compose --version

# Limpar containers antigos
docker-compose down -v
docker system prune -a
```

#### Porta já em uso
```bash
# Backend (porta 8000)
# Altere a porta no docker-compose.yml ou pare o processo usando a porta

# Frontend (porta 5173)
# Altere a porta no docker-compose.yml ou no vite.config.ts
```

#### Erro de dependências no Backend
```bash
# Reconstruir o ambiente
cd backend
rm -rf venv/  # ou pyBackEnd/
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

#### Erro de dependências no Frontend
```bash
# Limpar e reinstalar
cd frontend
rm -rf node_modules/
rm package-lock.json
npm install
```

## 📄 Licença

Este projeto está sob a licença especificada nos arquivos LICENSE nas pastas backend e frontend.

---

## 🤝 Contribuindo

Contribuições são bem-vindas! Sinta-se à vontade para:

1. Fazer fork do projeto
2. Criar uma branch para sua feature (`git checkout -b feature/MinhaFeature`)
3. Commit suas mudanças (`git commit -m 'Adiciona MinhaFeature'`)
4. Push para a branch (`git push origin feature/MinhaFeature`)
5. Abrir um Pull Request

---

## 📧 Contato

Para dúvidas ou sugestões, abra uma issue no repositório.

---

**Desenvolvido com ❤️ para análise financeira**

