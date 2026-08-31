---
title: "Como publicar neste blog (o fluxo de sempre)"
date: 2026-08-31 01:00:00 -0300
categories: [meta]
tags: [jekyll, git, workflow]
---

Este é o primeiro post de verdade — e nada melhor do que ele documentar o próprio fluxo que o publicou. Qualquer atualização no blog segue sempre os mesmos passos.

## Fluxo

```text
1. Editar o(s) arquivo(s) .md ou de configuração
2. git add -A
3. git commit -m "post: ..."
4. git push
5. Aguardar ~1 minuto. No ar.
```

O `push` em `main` dispara o GitHub Actions, que roda no meu próprio notebook: builda o Jekyll num container Ruby e publica a pasta `_site/` no nginx. Sem painel, sem banco, sem deploy manual.

## Exemplo real (31/08/2026): LinkedIn no rodapé + novo Sobre

Mudanças feitas neste dia, usadas como exemplo do fluxo:

### 1. Link do LinkedIn no rodapé (`_config.yml`)

O rodapé é configurado no `_config.yml`, na seção `social-network-links`:

```yaml
social-network-links:
  rss: true
  github: LeoCalvet
  linkedin: leonardo-calvet   # <- novo
```

No Beautiful Jekyll, `linkedin: leonardo-calvet` vira o link [linkedin.com/in/leonardo-calvet](https://www.linkedin.com/in/leonardo-calvet/) no rodapé, com ícone.

### 2. Novo texto da página Sobre (`sobre.md`)

A página vive em `sobre.md`, Markdown puro com front matter. O texto novo:

> Sou o Leonardo Calvet, desenvolvedor. Criei este blog para ser o backup dos meus delírios e ideias.
>
> Então espere de tudo: entre linguagens de programação, novas tecnologias, LLMs, filosofia e política. De tudo um pouco.

## Detalhe que importa

O **commit não publica; o push sim**. Posso commitar quantas vezes quiser localmente, mexer, revertar, escrever em rascunho (`_drafts/`) — nada sai enquanto não houver `git push`. Quando publico, cada push pode carregar vários commits de uma vez.

Um post é um arquivo `.md` em `_posts/` com data no nome, um commit e um push.
