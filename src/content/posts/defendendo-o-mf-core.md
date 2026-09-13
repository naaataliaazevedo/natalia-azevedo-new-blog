---
title: "Defendendo o mf-core: o shell de microfrontends não era óbvio pra todo mundo"
description: "Como argumentei a favor do mf-core como host de Module Federation contra a resistência do time, até alinhar com o CTO — e o que virou fitness function depois disso."
date: 2026-09-13
tags: ["mfe", "arquitetura", "frontend"]
draft: false
---

Quando comecei a puxar a migração de legado pra microfrontends, a primeira
decisão que precisei defender não foi técnica de verdade — foi política.
A proposta era simples no papel: ter um `mf-core` como shell, responsável
por orquestrar o Module Federation e expor os contratos que os
microfrontends filhos consumiriam. Na prática, teve resistência — inclusive
do Head de Tech.

## O argumento contra

A objeção mais forte era previsível: "mais uma camada é mais complexidade,
mais um ponto de falha, mais um lugar pra debugar quando algo quebra".
Não é um argumento errado — é o argumento certo pra qualquer decisão de
arquitetura que adiciona uma peça nova. O trabalho não era descartar essa
preocupação, era mostrar o que ela ignorava: sem um host formal, cada time
acaba reinventando sua própria forma de consumir os módulos remotos, e
você troca uma complexidade explícita por várias implícitas, espalhadas
e sem dono.

## Como cheguei no alinhamento

Não foi um documento de arquitetura que resolveu — foi mostrar o caminho
inverso: o que acontece daqui a um ano sem o shell. Múltiplos times
resolvendo o mesmo problema de formas diferentes, sem contrato comum entre
os remotes, sem lugar único pra aplicar regras de compatibilidade. Levar
essa discussão até o CTO ajudou a tirar a decisão do campo de opinião de
time e colocar no campo de risco de produto.

## O que virou prática depois

Depois do alinhamento, a parte mais interessante não foi o shell em si —
foi o que ele possibilitou em termos de *fitness functions* pra manter a
arquitetura íntegra com o tempo:

- **Limite de bundle size** para o shell e para cada MFE filho
- **Regras de `dependency-cruiser`** pra evitar acoplamento indevido entre módulos
- **Compatibilidade de schema GraphQL** entre o BFF e os consumidores
- **Checagens bloqueantes em CI/PR**, pra essas regras não dependerem de review manual

Nenhuma dessas coisas faz sentido sem um host central pra aplicá-las. O
shell não é só um detalhe técnico — é o lugar onde a arquitetura vira
regra executável, em vez de documentação que ninguém lê.

## O que eu levo disso

A parte técnica da decisão levou uma tarde pra desenhar. Convencer o time
levou semanas. Da próxima vez, tentaria trazer o "e se não fizermos isso"
pra mesa desde a primeira conversa, em vez de deixar pra usar como último
argumento.