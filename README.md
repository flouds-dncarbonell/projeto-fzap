# FZAP - WhatsApp Business API + Chatwoot Integration

<div align="center">

![FZAP Logo](https://via.placeholder.com/200x200/4CAF50/FFFFFF?text=FZAP)

**Enterprise-grade WhatsApp API with native Chatwoot integration**

[![Docker](https://img.shields.io/badge/Docker-Available-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/dncarbonell/fzap)
[![Version](https://img.shields.io/badge/Version-1.6.1-success)](https://github.com/flouds-dncarbonell/fzap)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Go](https://img.shields.io/badge/Go-1.21+-00ADD8?logo=go&logoColor=white)](https://golang.org/)

[Features](#-principais-funcionalidades) • [Quick Start](#-quick-start) • [Documentation](#-documentação) • [Docker](#-docker-hub) • [Support](#-suporte)

</div>

---

## 📋 Sobre o Projeto

**FZAP** é uma solução empresarial completa para integração WhatsApp Business, construída sobre a biblioteca [@tulir/whatsmeow](https://github.com/tulir/whatsmeow) com uma **integração nativa e bidirecional com Chatwoot**.

Diferente de outras soluções que usam Puppeteer ou emuladores Android, o FZAP se conecta diretamente aos servidores WebSocket do WhatsApp, resultando em:

- ⚡ **Performance superior** - Menor uso de CPU e memória
- 🚀 **Velocidade** - Respostas instantâneas sem overhead de navegador
- 💪 **Estabilidade** - Conexão direta sem camadas intermediárias
- 🔧 **Escalabilidade** - Suporte a múltiplas instâncias simultâneas

---

## ✨ Principais Funcionalidades

### 🎯 Integração Chatwoot Nativa

A grande diferença do FZAP: **integração Chatwoot 100% nativa em Go**, sem necessidade de serviços externos ou middlewares.

- ✅ **Fluxo Bidirecional Completo** - WhatsApp ↔ Chatwoot sincronizado
- ✅ **Todos os Tipos de Mídia** - Imagens, vídeos, áudios, documentos, stickers
- ✅ **Áudios PTT** - Conversão automática de áudios de voz (MP3 → OGG Opus)
- ✅ **Sistema de Quotes** - Respostas e citações bidirecionais
- ✅ **Edição e Exclusão** - Sincronização automática de mensagens editadas/deletadas
- ✅ **Comandos de Bot** - `/init`, `/status`, `/clearcache`, `/disconnect`
- ✅ **Dashboard Web** - Interface completa para configuração

### 🚀 API WhatsApp Completa

- 📱 **Sessões Múltiplas** - Gerencie várias contas WhatsApp no mesmo servidor
- 💬 **Mensagens** - Texto, mídia, localização, contatos, enquetes
- 👥 **Grupos** - Criação, gerenciamento, convites, participantes
- 📞 **Presença** - Status de digitação, gravação de áudio
- 📊 **Webhooks** - Sistema avançado com subscrição de eventos
- 🔐 **Autenticação** - Sistema de tokens por usuário

### 🎨 Features Empresariais

- **RabbitMQ Integration** - Distribuição global de eventos com fallback automático
- **S3 Storage** - Integração completa para armazenamento de mídias
- **Proxy Support** - Configuração de proxy por usuário
- **Smart Contact Management** - Auto-detecção e merge de contatos brasileiros
- **Message Recovery** - Recuperação automática de mensagens perdidas
- **Queue System** - Filas por contato eliminam race conditions
- **Branding Customizável** - Nome de plataforma e identificadores personalizáveis

### 📈 Performance & Confiabilidade

- **Cache Inteligente** - Sistema de cache com TTL e auto-invalidação
- **Anti-Loop Protection** - Múltiplas camadas de prevenção
- **Smart Retry** - Retry inteligente com pausas estratégicas
- **Queue Monitoring** - Status em tempo real das filas de mensagens
- **Auto Checkpoints** - Checkpoints automáticos para recuperação

---

## 🚀 Quick Start

### Docker (Recomendado)

```bash
# Pull da imagem
docker pull dncarbonell/fzap:latest

# Executar com SQLite
docker run -d -p 8080:8080 \
  -e DB_TYPE=sqlite \
  -e WUZAPI_ADMIN_TOKEN=seu_token_admin \
  -v $(pwd)/data:/app/data \
  dncarbonell/fzap:latest

# Acessar dashboard
open http://localhost:8080/dashboard
```

### Configuração Inicial

1. **Acesse o Dashboard:** `http://localhost:8080/dashboard`
2. **Crie um usuário** via API Admin ou dashboard
3. **Conecte o WhatsApp** escaneando o QR Code
4. **Configure o Chatwoot** (opcional):
   - URL da instância Chatwoot
   - Account ID
   - API Token
   - Ativar integração

### Primeiros Passos

```bash
# Criar usuário via API
curl -X POST http://localhost:8080/admin/users \
  -H "Authorization: seu_token_admin" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "Minha Empresa",
    "token": "token_usuario",
    "webhook": "https://webhook.site/...",
    "events": "All"
  }'

# Obter QR Code
curl http://localhost:8080/session/qr/image \
  -H "Authorization: token_usuario"

# Enviar mensagem
curl -X POST http://localhost:8080/message/text \
  -H "Authorization: token_usuario" \
  -H "Content-Type: application/json" \
  -d '{
    "phone": "5511999999999",
    "message": "Olá do FZAP!"
  }'
```

---

## 🐳 Docker Hub

Imagens oficiais disponíveis no Docker Hub:

**Repository:** [`dncarbonell/fzap`](https://hub.docker.com/r/dncarbonell/fzap)

```bash
# Versão específica (recomendado para produção)
docker pull dncarbonell/fzap:v1.6.1

# Sempre a versão mais recente
docker pull dncarbonell/fzap:latest
```

### Tags Disponíveis

- `latest` - Última versão estável
- `v1.6.1` - Versão 1.6.1 (Stability & Improvements)
- `v1.6.0` - Versão 1.6.0 (Enhanced Integration & Webhook System)
- `v1.5.0` - Versão 1.5.0 (Production Ready Release)

---

## ⚙️ Configuração

### Variáveis de Ambiente Essenciais

```env
# Essencial
WUZAPI_ADMIN_TOKEN=seu_token_admin_aqui
DB_TYPE=sqlite
TZ=America/Sao_Paulo

# Chatwoot
FZAP_SYSTEM_IDENTIFIER=suaempresa.com.br
PLATFORM_NAME=SuaPlataforma

# Performance
MAX_FILE_SIZE_MB=100
DOWNLOAD_TIMEOUT_SECONDS=120
MESSAGE_DELIVERY_TIMEOUT_MINUTES=30
IMAGE_QUALITY_HD=false

# RabbitMQ (opcional)
RABBITMQ_ENABLED=true
RABBITMQ_URL=amqp://guest:guest@rabbitmq:5672
```

### PostgreSQL (Opcional)

```env
DB_TYPE=postgres
DB_USER=fzap
DB_PASSWORD=senha_segura
DB_NAME=fzap
DB_HOST=postgres
DB_PORT=5432
```

---

## 📚 Documentação

### Interfaces Web

- **Dashboard Completo:** `http://localhost:8080/dashboard`
  - Gerenciamento de instâncias
  - Configuração Chatwoot
  - Testes de integração

- **API Reference (Swagger):** `http://localhost:8080/api`
  - Documentação interativa
  - Testes de endpoints

- **Login QR Code:** `http://localhost:8080/login`
  - Scan rápido de QR Code

### Endpoints Principais

#### Admin
- `GET /admin/users` - Listar usuários
- `POST /admin/users` - Criar usuário
- `DELETE /admin/users/{id}` - Remover usuário

#### Sessão
- `GET /session/status` - Status da conexão
- `GET /session/qr/image` - QR Code para scan
- `POST /session/disconnect` - Desconectar
- `POST /session/logout` - Logout completo

#### Mensagens
- `POST /message/text` - Enviar texto
- `POST /message/image` - Enviar imagem
- `POST /message/audio` - Enviar áudio
- `POST /message/document` - Enviar documento
- `POST /message/video` - Enviar vídeo

#### Chatwoot
- `POST /chatwoot/config` - Configurar integração
- `GET /chatwoot/status` - Status e filas
- `POST /chatwoot/test-connection` - Testar conexão
- `POST /chatwoot/webhook` - Receber eventos

---

## 🏗️ Arquitetura

### Estrutura do Projeto

```
fzap/
├── main.go                 # Entry point
├── handlers.go             # API endpoints
├── middlewares.go          # Auth & logging
├── models.go               # Database models
├── chatwoot/              # 🎯 Integração Chatwoot
│   ├── chatwoot.go        # Entry point
│   ├── client.go          # HTTP client
│   ├── processor.go       # WhatsApp → Chatwoot
│   ├── webhook.go         # Chatwoot → WhatsApp
│   ├── media.go           # Processamento de mídias
│   ├── messages.go        # Sistema de quotes
│   ├── cache.go           # Cache com TTL
│   └── handlers.go        # REST endpoints
├── rabbitmq/              # Sistema RabbitMQ
├── s3client/              # Cliente S3
└── static/                # Dashboard web
```

### Fluxo de Mensagens

```
WhatsApp → FZAP → Chatwoot
    ↑                ↓
    └────────────────┘
    (Bidirecional completo)
```

1. **WhatsApp → Chatwoot:**
   - Evento recebido via whatsmeow
   - Processamento de mídia (download, conversão)
   - Criação/busca de contato no Chatwoot
   - Criação/busca de conversa
   - Envio de mensagem formatada

2. **Chatwoot → WhatsApp:**
   - Webhook recebido do Chatwoot
   - Validação e deduplicação
   - Processamento de quotes/replies
   - Envio via whatsmeow
   - Tracking de entrega

---

## 🔒 Segurança

### Melhores Práticas

1. **Tokens Fortes:** Use tokens aleatórios e complexos
2. **HTTPS:** Configure SSL/TLS para produção
3. **Firewall:** Restrinja acesso aos endpoints admin
4. **Rate Limiting:** Configure limites de requisições
5. **Backups:** Mantenha backups regulares do banco de dados

### Avisos Importantes

⚠️ **WhatsApp Terms of Service**

O uso desta ferramenta para SPAM ou violação dos Termos de Serviço do WhatsApp pode resultar no **banimento permanente do seu número**.

- ❌ Não envie mensagens não solicitadas
- ❌ Não faça disparo em massa sem opt-in
- ❌ Não use para práticas abusivas

Para uso comercial em grande escala, considere usar a **WhatsApp Business API oficial**.

---

## 🎯 Casos de Uso

### 1. Atendimento ao Cliente
- Integração com Chatwoot para centralizar conversas
- Múltiplos atendentes respondendo pelo mesmo número
- Histórico completo de conversas

### 2. Automação
- Respostas automáticas via webhooks
- Integração com CRM/ERP
- Notificações e alertas

### 3. Chatbots
- Implementação de bots inteligentes
- Integração com IA (GPT, etc.)
- Fluxos de conversa automatizados

### 4. Notificações
- Alertas de sistemas
- Confirmações de pedidos
- Status de entregas

---

## 📊 Versões

### v1.6.1 - Stability & Improvements (Atual)
- Melhorias de estabilidade
- Correções de bugs
- Otimizações de performance

### v1.6.0 - Enhanced Integration & Webhook System
- Sistema de timeout configurável
- Integração S3 bidirecional avançada
- Sistema de webhook externo
- Branding system aprimorado
- Processamento inteligente de imagens

### v1.5.0 - Production Ready Release
- Sistema RabbitMQ global
- Brazilian Contact Intelligence
- Enhanced Avatar System
- Smart Typing Feature

### v1.4.0 - RabbitMQ Integration
- Integração completa RabbitMQ
- FZAP Welcome System
- Enhanced Self-Contact

[Ver histórico completo →](https://github.com/flouds-dncarbonell/fzap/blob/main/CLAUDE.md)

---

## 🛠️ Suporte

### Recursos

- 📖 **Documentação:** Swagger API em `/api`
- 💬 **Issues:** [GitHub Issues](https://github.com/flouds-dncarbonell/fzap/issues)
- 📧 **Email:** dncarbonell@flouds.com.br
- 🐳 **Docker Hub:** [dncarbonell/fzap](https://hub.docker.com/r/dncarbonell/fzap)

### Repositório Principal

O código-fonte está disponível em:
**[github.com/flouds-dncarbonell/fzap](https://github.com/flouds-dncarbonell/fzap)**

### Desenvolvimento

FZAP é baseado no excelente projeto [WuzAPI](https://github.com/asternic/wuzapi) por Nicolás Gudiño, com melhorias e integração Chatwoot por Diego Carbonell.

---

## 📝 License

**MIT License**

Copyright (c) 2025 Diego Carbonell (FZAP enhancements)
Copyright (c) 2025 Nicolás Gudiño (Original WuzAPI)

Consulte o arquivo [LICENSE](LICENSE) para mais detalhes.

---

## ⚖️ Legal

Este software não é afiliado, autorizado, mantido, patrocinado ou endossado pelo WhatsApp ou qualquer uma de suas afiliadas ou subsidiárias. Este é um software independente e não oficial.

**Use por sua conta e risco.**

---

## 🙏 Agradecimentos

- [@tulir](https://github.com/tulir) - Biblioteca whatsmeow
- [Nicolás Gudiño](https://github.com/asternic) - Projeto original WuzAPI
- Todos os [contribuidores](https://github.com/asternic/wuzapi/graphs/contributors) do WuzAPI

---

## 🌟 Star History

### WuzAPI (Projeto Original)
[![Star History Chart](https://api.star-history.com/svg?repos=asternic/wuzapi&type=Date)](https://www.star-history.com/#asternic/wuzapi&Date)

---

<div align="center">

**Made with ❤️ by Diego Carbonell**

[🏠 Home](https://github.com/flouds-dncarbonell/projeto-fzap) • [📦 Releases](https://github.com/flouds-dncarbonell/fzap/releases) • [🐳 Docker Hub](https://hub.docker.com/r/dncarbonell/fzap)

</div>