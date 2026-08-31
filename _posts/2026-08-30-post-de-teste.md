---
title: "Post de teste — como o blog renderiza"
date: 2026-08-30 22:00:00 -0300
categories: [teste]
tags: [exemplo]
---

Este post existe só pra você avaliar o visual. Pode deletar quando quiser (`git rm _posts/2026-08-30-post-de-teste.md`).

## Texto e formatação

Parágrafo normal com **negrito**, *itálico* e `código inline`. Um [link](https://jekyllrb.com) pra ver a cor. Lorem ipsum dolor sit amet, consectetur adipiscing elit — texto corrido pra avaliar a leitura em 17px com a CaskaydiaCove.

> Citação em bloco, pro estilo dela também aparecer.

## Código (Ruby, claro)

```ruby
class Blog
  def initialize(author:)
    @author = author
  end

  def publicar!(post)
    puts "#{@author} publicou: #{post.titulo}"
  end
end
```

## Lista

1. Primeiro item
2. Segundo item com um pouco mais de texto pra quebrar linha
   - sub-item aninhado
   - outro sub-item

## Tabela

| Serviço | Porta | Status |
|---|---|---|
| nginx | 8095 | no ar |
| n8n | 5678 | no ar |
| Beszel | 8090 | no ar |
