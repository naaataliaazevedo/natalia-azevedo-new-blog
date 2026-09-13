---
title: "Versionando um Design System em escala sem travar os times"
description: "Como manter duas versões de um Design System em paralelo — uma v1 com breaking changes e uma linha legada — sem bloquear entregas."
date: 2026-09-12
tags: ["design-system", "frontend", "versionamento"]
draft: false
---

É possível manter duas versões de um Design System em paralelo sem
quebrar os times que dependem dele. Quando um DS evolui pra uma v1 com
breaking changes — novos tokens, novas foundations, arquitetura diferente
— nem todos os produtos vão conseguir migrar no mesmo ritmo. E tudo bem:
o problema não é a velocidade diferente, é não ter um plano pra ela.

## A estrutura de branches

Uma abordagem que funciona bem em times de plataforma é organizar duas
linhas paralelas:

main → v1.0.0, v1.0.1… (nova versão)
release/0.x → 0.0.24, 0.0.25… (linha legada)


Na prática:

- Crie a `release/0.x` antes de começar a trabalhar na v1
- Bugs críticos na versão antiga entram como fix direto na `release/0.x`
- Novas features e evoluções de arquitetura só acontecem na v1

## Como isso aparece no registry

@seu-ds/core
├── 0.0.23
├── 0.0.24 ← fix legado
├── 1.0.0 ← nova arquitetura
└── 1.0.1


Cada produto migra quando estiver pronto — sem pressa, sem bloquear
entregas, sem forçar um squad a absorver uma breaking change no meio de
uma sprint que não tem espaço pra isso.

## Por que isso é diferente de "só seguir semver"

Semver resolve o versionamento em teoria. O que resolve na prática é ter
um processo definido pra decidir onde cada tipo de mudança entra — fix
crítico na linha legada, evolução estrutural na nova — e comunicar isso
com clareza pros times que consomem o pacote. Sem esse processo, versionar
certo não impede que a migração vire um bloqueio de qualquer jeito.