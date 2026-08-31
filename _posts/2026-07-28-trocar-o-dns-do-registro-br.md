---
title: "Delegando o DNS do Registro.br para a Cloudflare"
date: 2026-07-28 10:00:00 -0300
categories: [home server]
tags: [dns, cloudflare, registro.br]
excerpt: "Registro do domínio e gerenciamento de DNS são funções distintas — e entender isso mudou tudo."
---

Registro do domínio e gerenciamento de DNS são funções distintas. O **Registro.br** continua responsável pela propriedade, renovação e dados cadastrais, enquanto a **Cloudflare** passou a responder pelos registros DNS. Não houve transferência do domínio para outro registrador.

## Os nameservers

A Cloudflare atribuiu `nora.ns.cloudflare.com` e `oswald.ns.cloudflare.com`. No painel do Registro.br, os servidores anteriores (`a.auto.dns.br` e `b.auto.dns.br`) foram substituídos — essa operação delegou a zona DNS para a Cloudflare.

## A pegadinha do DNSSEC

Antes da troca, valeu conferir o DNSSEC: um registro DS antigo no registrador apontando para chaves que deixaram de existir poderia tornar o domínio *aparentemente inexistente* para resolvedores com validação. Não havia configuração ativa que impedisse a troca — seguimos em frente.

## O intervalo estranho

Depois de salvar, a Cloudflare exibiu o domínio como pendente por um tempo. Isso é normal: a delegação publicada ainda estava em transição. A preparação do notebook seguiu em paralelo — afinal, instalar Docker e cloudflared não depende de DNS.
