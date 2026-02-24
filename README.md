# FZAP - WhatsApp Business API para operacao profissional

<div align="center">

![FZAP Version](https://img.shields.io/badge/Version-1.15.3-success)
[![Docker](https://img.shields.io/badge/Docker-Available-2496ED?logo=docker&logoColor=white)](https://hub.docker.com/r/dncarbonell/fzap)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](https://github.com/flouds-dncarbonell/fzap/blob/main/LICENSE)

**API WhatsApp completa com integracao nativa ao Chatwoot, Cloud API e Typebot**

[Recursos](#-recursos) • [Deploy](#-deploy) • [Aquisição](#-aquisição-da-fzap) • [Links](#-links-uteis)

</div>

---

## Sobre

O **FZAP** e uma plataforma de mensageria WhatsApp para operacoes de atendimento, vendas e automacao.

Baseado em `whatsmeow`, conecta diretamente no WhatsApp sem navegador/emulador e adiciona recursos de operacao:

- Integracao bidirecional com **Chatwoot**
- Suporte **multi-provider**: Whatsmeow e **Meta Cloud API**
- Integracao nativa com **Typebot**
- Dashboard web para operacao e configuracao
- Webhooks, filas, proxy, S3 e recursos para ambiente de producao

Versao de referencia atual: **v1.15.3**.

---

## Recursos

- **WhatsApp API completa**: texto, imagem, audio, video, documento, contato, localizacao, enquetes, interativos (buttons/list/carousel), status/stories, grupos e comunidades.
- **Chatwoot nativo**: sincronizacao de mensagens e midias, quote, edicao/exclusao, comandos de bot e importacao de historico.
- **Cloud API (Meta)**: conexao por `providerType=cloudapi` e webhook publico `GET/POST /webhook/meta/{user_token}`.
- **Typebot nativo**: CRUD de bots, sessoes e gatilhos por API.
- **Escalabilidade**: RabbitMQ opcional com fallback automatico.
- **Armazenamento**: suporte a S3 por instancia.
- **Rede**: proxy por instancia com rotacao.
- **White-label**: `PLATFORM_NAME`, `FZAP_SYSTEM_NAME`, `FZAP_SYSTEM_IDENTIFIER`.

---

## Deploy

### Imagem Docker

```bash
docker pull dncarbonell/fzap:latest
# ou fixa
docker pull dncarbonell/fzap:v1.15.3
```

### Execucao rapida (minima)

```bash
docker run -d -p 8080:8080 \
  -e ADMIN_TOKEN=troque-este-token \
  -e TZ=America/Sao_Paulo \
  -v $(pwd)/dbdata:/app/dbdata \
  dncarbonell/fzap:latest
```

### Stack completa

A stack completa (Swarm/Traefik/PostgreSQL/RabbitMQ/volumes/rede) esta neste arquivo:

- [stack.yml](https://github.com/flouds-dncarbonell/projeto-fzap/blob/main/stack.yml)

---

## Interfaces

- Dashboard v2: `http://localhost:8080/dashboard`
- Dashboard legado: `http://localhost:8080/legacy`
- Swagger/API: `http://localhost:8080/api`

---

## Licenciamento

O FZAP inicia em **modo Free** sem `FLOUDS_LICENCE_KEY`.

Com licenca ativa, recursos premium ficam habilitados conforme plano contratado.

---

## Aquisição da FZAP

Para **adquirir a FZAP** (licenca, implantacao e suporte):

- **Email:** `daniel@flouds.com.br`
- **WhatsApp:** `+55 51 99864-1731`

Se preferir, abra contato por este repositorio e enviamos proposta com o escopo do seu ambiente.

---

## Links uteis

- Codigo-fonte do produto: [flouds-dncarbonell/fzap](https://github.com/flouds-dncarbonell/fzap)
- Docker Hub: [dncarbonell/fzap](https://hub.docker.com/r/dncarbonell/fzap)
- Documentacao interativa: `/api` na sua instancia

