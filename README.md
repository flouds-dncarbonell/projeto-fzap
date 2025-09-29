# FZAP - WhatsApp Business API + Chatwoot Integration

<div align="center">

![FZAP Version](https://img.shields.io/badge/Version-1.6.1-success)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Docker](https://img.shields.io/badge/Docker-Available-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/dncarbonell/fzap)

**Solução empresarial completa para WhatsApp Business com integração nativa ao Chatwoot**

[Sobre](#-sobre-o-fzap) • [Recursos](#-recursos-principais) • [Docker](#-docker) • [Documentação](#-documentação) • [Suporte](#-suporte)

</div>

---

## 📋 Sobre o FZAP

**FZAP** é uma API REST completa para WhatsApp Business que oferece integração nativa e bidirecional com o **Chatwoot**, permitindo centralizar todo o atendimento via WhatsApp em uma plataforma moderna de customer service.

Construído sobre a biblioteca [@tulir/whatsmeow](https://github.com/tulir/whatsmeow), o FZAP se conecta diretamente aos servidores do WhatsApp sem usar navegadores ou emuladores, garantindo:

- ⚡ **Alta Performance** - Baixo consumo de recursos
- 🚀 **Velocidade** - Comunicação direta com WhatsApp
- 💪 **Estabilidade** - Conexão nativa sem intermediários
- 🔧 **Escalabilidade** - Suporte a múltiplas instâncias

---

## ✨ Recursos Principais

### 🎯 Integração Chatwoot Nativa

O grande diferencial do FZAP: **integração completa e bidirecional com Chatwoot**.

- ✅ **Sincronização Total** - WhatsApp ↔ Chatwoot em tempo real
- ✅ **Todas as Mídias** - Imagens, vídeos, áudios, documentos, stickers
- ✅ **Mensagens de Voz** - Suporte completo para PTT (Push-to-Talk)
- ✅ **Respostas e Citações** - Sistema de quotes bidirecional
- ✅ **Edição e Exclusão** - Sincronização de alterações
- ✅ **Gerenciamento de Contatos** - Auto-detecção e merge inteligente
- ✅ **Comandos de Bot** - Controle direto pelo Chatwoot
- ✅ **Interface Web** - Dashboard completo para configuração

### 💬 API WhatsApp Completa

- **Mensagens:** Texto, mídia, localização, contatos, enquetes
- **Grupos:** Criação, gerenciamento, convites
- **Sessões:** Múltiplas contas simultâneas
- **Presença:** Status de digitação, online/offline
- **Webhooks:** Sistema avançado de notificações
- **Autenticação:** Tokens individuais por instância

### 🚀 Recursos Empresariais

- **Filas de Mensagens** - Eliminação total de race conditions
- **Recuperação Automática** - Sistema inteligente de recovery
- **Cache Avançado** - Performance otimizada
- **Armazenamento S3** - Integração opcional para mídias
- **RabbitMQ** - Distribuição de eventos em larga escala
- **Proxy Support** - Configuração por instância
- **Customização** - Branding personalizável

---

## 🐳 Docker

FZAP está disponível como imagem Docker pronta para uso:

### Docker Hub

**Registry:** [`dncarbonell/fzap`](https://hub.docker.com/r/dncarbonell/fzap)

```bash
# Última versão estável
docker pull dncarbonell/fzap:latest

# Versão específica
docker pull dncarbonell/fzap:v1.6.1
```

### Quick Start

```bash
docker run -d -p 8080:8080 \
  -e WUZAPI_ADMIN_TOKEN=seu_token_seguro \
  -v $(pwd)/data:/app/data \
  dncarbonell/fzap:latest
```

Acesse: `http://localhost:8080/dashboard`

---

## 📚 Documentação

### Interfaces Web

Após iniciar o FZAP, acesse:

- **Dashboard:** `http://localhost:8080/dashboard`
  - Gerenciamento completo de instâncias
  - Configuração da integração Chatwoot
  - Testes e monitoramento

- **API Documentation:** `http://localhost:8080/api`
  - Documentação Swagger interativa
  - Testes de endpoints

- **QR Code Login:** `http://localhost:8080/login`
  - Conexão rápida ao WhatsApp

### Configuração Chatwoot

1. Acesse o Dashboard
2. Configure sua instância Chatwoot:
   - URL da instância
   - Account ID
   - API Token
3. Ative a integração
4. Pronto! Mensagens sincronizadas automaticamente

### Comandos de Bot

Execute comandos diretamente no Chatwoot:

- `/init` - Conectar ao WhatsApp
- `/status` - Ver status da conexão
- `/clearcache` - Limpar cache
- `/disconnect` - Desconectar

---

## 🎯 Casos de Uso

### Atendimento ao Cliente
Centralize todas as conversas WhatsApp no Chatwoot, permitindo múltiplos atendentes responderem pelo mesmo número.

### Automação
Integre com sistemas externos via webhooks para criar fluxos automatizados de resposta e notificação.

### Chatbots
Desenvolva bots inteligentes com integração a IA (GPT, DialogFlow, etc.) através da API REST.

### Notificações
Envie alertas, confirmações e atualizações de forma programática para seus clientes.

---

## ⚙️ Configuração

### Variáveis de Ambiente

```env
# Essencial
WUZAPI_ADMIN_TOKEN=seu_token_admin
DB_TYPE=sqlite

# Opcional - Branding
FZAP_SYSTEM_IDENTIFIER=suaempresa.com
PLATFORM_NAME=SuaPlataforma

# Opcional - Performance
MAX_FILE_SIZE_MB=100
DOWNLOAD_TIMEOUT_SECONDS=120
MESSAGE_DELIVERY_TIMEOUT_MINUTES=30
```

Para uso com PostgreSQL, RabbitMQ ou S3, consulte a documentação completa na API.

---

## 🔒 Segurança e Compliance

### ⚠️ Aviso Importante

O uso do FZAP deve estar em conformidade com os **Termos de Serviço do WhatsApp**.

**Não permitido:**
- ❌ Envio de SPAM
- ❌ Mensagens em massa não solicitadas
- ❌ Práticas abusivas

**Violações podem resultar no banimento permanente do número.**

Para uso comercial em larga escala, considere a **WhatsApp Business API oficial**.

### Boas Práticas

- Use tokens seguros e complexos
- Configure HTTPS em produção
- Implemente rate limiting
- Faça backups regulares
- Monitore logs de uso

---

## 📊 Versões

### 🎉 v1.6.1 - Atual
Melhorias de estabilidade e performance

### 🚀 v1.6.0
Sistema avançado de webhooks e integração S3

### 💪 v1.5.0
Produção ready com RabbitMQ global

### ⚡ v1.4.0
Integração RabbitMQ e sistema de boas-vindas

[Ver changelog completo →](https://github.com/flouds-dncarbonell/fzap)

---

## 🛠️ Suporte

### Recursos Disponíveis

- 📖 **Documentação API:** Swagger em `/api`
- 🐳 **Docker Hub:** [dncarbonell/fzap](https://hub.docker.com/r/dncarbonell/fzap)
- 💻 **Código Fonte:** [GitHub](https://github.com/flouds-dncarbonell/fzap)
- 💬 **Issues:** [GitHub Issues](https://github.com/flouds-dncarbonell/fzap/issues)

---

## 🌟 Star History

### WuzAPI (Projeto Base)
[![Star History Chart](https://api.star-history.com/svg?repos=asternic/wuzapi&type=Date)](https://www.star-history.com/#asternic/wuzapi&Date)

---

## 📝 Licença

**MIT License**

- **FZAP** - Desenvolvido por Daniel Carbonell
- **WuzAPI** - Projeto original por Nicolás Gudiño

---

## ⚖️ Legal

Este software não é afiliado, autorizado, mantido, patrocinado ou endossado pelo WhatsApp ou qualquer uma de suas afiliadas. Este é um software independente e não oficial.

**Use por sua conta e risco.**

---

## 🙏 Créditos

- **Daniel Carbonell** - Desenvolvimento FZAP e integração Chatwoot
- **[@tulir](https://github.com/tulir)** - Biblioteca whatsmeow
- **[Nicolás Gudiño](https://github.com/asternic)** - Projeto WuzAPI original
- Todos os [contribuidores](https://github.com/asternic/wuzapi/graphs/contributors) do WuzAPI

---

<div align="center">

**Desenvolvido por Daniel Carbonell**

[📦 Docker Hub](https://hub.docker.com/r/dncarbonell/fzap) • [💻 GitHub](https://github.com/flouds-dncarbonell/fzap) • [📖 Documentação](http://localhost:8080/api)

</div>