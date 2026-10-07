# Flux v1: modelo de caixas

> **Versão arquivada.** Esta é a primeira versão do [Flux](https://github.com/Alex1Ribas/Flux), mantida só como registro da evolução do projeto. A versão atual passou por um redesenho de produto e está no repositório principal.

## A ideia

A v1 organizava o dinheiro em **caixas** (envelopes). A pergunta central do app era:

> "De qual parte do meu patrimônio esse dinheiro saiu?"

Existiam três tipos de caixa:

- **Origem**: onde a receita entra (ex.: Salário).
- **Objetivo**: meta de acúmulo com aporte mensal planejado.
- **Orçamento**: envelope com limite mensal de gastos (limites diário e semanal derivados).

O fluxo seguia **origem → distribuição → alocação → pagamento**:

- Toda entrada creditava uma caixa de origem e depois era **distribuída** para as caixas de alocação.
- Toda saída debitava uma caixa, respeitando `disponível = saldo − comprometido`.
- Compras no cartão não debitavam na hora: geravam **comprometimento** até a fatura.
- Contas a pagar comprometiam o saldo até serem **liquidadas**.

Além disso: lançamentos recorrentes e parcelados, empréstimos, orçamento por competência, acompanhamento mensal com indicador de risco, simulação de impacto de uma decisão e categorias personalizadas.

## Por que foi substituída

Usando o app no dia a dia, o modelo se mostrou trabalhoso demais: cada movimentação precisava ser registrada, distribuída e liquidada. O custo de manter os dados em dia era maior que o valor da resposta.

A [v2](https://github.com/Alex1Ribas/Flux) troca o registro do passado pelo planejamento do futuro: você descreve rendas e contas, e o app projeta os próximos meses e responde **"quanto posso gastar agora sem comprometer o resto?"**.

| | v1 (este repo) | v2 |
|---|---|---|
| Modelo | Caixas + lançamentos | Rendas + contas + reserva |
| Operações da API | 35 | 11 |
| Código (front + back) | ~19,8 mil linhas | ~6,7 mil linhas |
| Telas | 10 | 4 |

## Stack

- **Frontend**: Expo / React Native com Expo Router, TanStack Query, Zustand, NativeWind e Moti.
- **Backend**: Express 5 + MongoDB em Clean Architecture, com contrato OpenAPI validado em runtime.
- **Deploy**: Vercel (API + web) e EAS com OTA updates.

## Histórico

O app começou como **finCaixas**, com frontend e API em repositórios separados, e foi unificado neste monorepo em julho de 2026. O histórico de commits deste repo vai de julho a agosto de 2026, até o início do redesenho.

> Este código compartilha a identidade de deploy (EAS `projectId`, canal OTA, API) com a versão atual. Antes de gerar qualquer build a partir dele, troque `name`, `slug`, `bundleIdentifier`/`package` e `projectId` em `Frontend/app.json`.

## Licença

[MIT](LICENSE) © Alex Ribas
