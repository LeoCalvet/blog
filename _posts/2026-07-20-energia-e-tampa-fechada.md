---
title: "Notebook com a tampa fechada, sem suspender"
date: 2026-07-20 19:30:00 -0300
categories: [home server]
tags: [pop-os, systemd, logind]
excerpt: "Como ensinar o systemd-logind a ignorar a tampa fechada — só quando estiver na tomada."
---

O plano era simples: o notebook deveria continuar utilizável como computador pessoal, mas na maior parte do tempo permanecer ligado como host Docker. Fechar a tampa na tomada não podia suspender a máquina.

## A configuração

Criamos `/etc/systemd/logind.conf.d/10-home-server.conf`:

```ini
HandleLidSwitch=suspend
HandleLidSwitchExternalPower=ignore
HandleLidSwitchDocked=ignore
```

Com isso, fechar a tampa **usando bateria** continua suspendendo — mas na tomada ou na dock, o logind ignora.

## Validação

Sessenta conexões SSH em intervalos de cinco segundos, verificando o `boot_id` e o estado do Docker a cada uma. Todas passaram: mesmo `boot_id`, Docker `active`, tampa fechada. Uma tela apagada não interrompe processos; suspensão interromperia.
