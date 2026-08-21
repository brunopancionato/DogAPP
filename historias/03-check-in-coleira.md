> Parte de **[CãoMetria — primeira fatia](historias-caometria-primeira-fatia.md)**.
> Contexto, escopo, premissas e perguntas em aberto estão no índice.

# História 3 — Registrar a chegada do pet e receber a instrução da coleira

**Prioridade:** P0
**Depende de:** História 2

> **Como** atendente da creche
> **quero** registrar quem chegou e ser instruído sobre qual coleira colocar
> **para que** o risco de cada cão fique visível do outro lado do salão, sem ninguém
> precisar consultar tela

### Critérios de aceite

**CA1 — instrução clara antes de confirmar**
```gherkin
Dado que a Nina chegou e está na lista de ausentes
Quando a seleciono no check-in
Então vejo em destaque "Coleira AMARELA" com o nome dela
E vejo o resumo dos apontamentos do dia ("remédio 14:00 · comida 12:00 · alergia: frango")
```

**CA2 — pet reativo reforça o manejo**
```gherkin
Dado que o Thor é reativo
Quando abro a confirmação de chegada dele
Então além da coleira VERMELHA vejo a observação de manejo do prontuário
E o reforço de isolamento aparece antes do botão de confirmar
```

**CA3 — confirmação coloca o pet no painel**
```gherkin
Dado que estou na tela de instrução da coleira
Quando confirmo a presença
Então o pet passa a constar no Painel do dia
E deixa de aparecer na lista de check-in
```

**CA4 — desistir não registra**
```gherkin
Dado que abri a instrução da coleira por engano
Quando volto sem confirmar
Então o pet continua ausente e nada é registrado
```

**CA5 — todos já chegaram**
```gherkin
Dado que todos os pets cadastrados já tiveram check-in hoje
Quando abro o check-in
Então vejo a mensagem de que não há pets pendentes de chegada
```

### Fora desta história
- Busca por nome na lista de chegada — ver pergunta em aberto #6.
- Registrar quem trouxe o pet (o simétrico do check-out) — não foi pedido.
