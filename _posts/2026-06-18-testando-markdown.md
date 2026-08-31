---
title: "Markdown: o que um post suporta"
date: 2026-06-18 14:00:00 -0300
categories: [meta]
tags: [markdown, teste]
excerpt: "Listas de tarefa, código, tabelas, citações — um passeio pela sintaxe suportada."
---

## Lista de tarefas

- [x] Escolher o gerador (Jekyll)
- [x] Registrar o domínio
- [ ] Escrever o primeiro post de verdade
- [ ] Criar a rota no Cloudflare Tunnel

## Código inline vs bloco

Use `bundle exec jekyll build` para validar, e:

```yaml
# compose.yaml — o padrão da casa
services:
  web:
    image: nginx:alpine
    ports:
      - "127.0.0.1:8095:80"
```

## Citações aninhadas

> Primeiro nível
> > Segundo nível — só pra ver a renderização
