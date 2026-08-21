> Parte de **[CãoMetria — primeira fatia](historias-caometria-primeira-fatia.md)**.
> Contexto, escopo, premissas e perguntas em aberto estão no índice.

# História 10 — Ver a dose atrasada escalar no painel

**Prioridade:** P1
**Depende de:** História 7

> **Como** atendente da creche
> **quero** que uma dose vencida fique gritando no painel
> **para que** o atraso apareça mesmo para quem não ouviu o alarme — e eu saiba o que
> cobrar agora

### Critérios de aceite

**CA1 — atraso marcado no card**
```gherkin
Dado que a dose da Nina estava agendada para 14:00 e são 14:12
Quando olho o Painel do dia
Então o card dela mostra "dose atrasada · 14:12" em destaque de alerta
E ela aparece no topo da lista, à frente dos demais pets da mesma cor
```

**CA2 — contagem de atrasos**
```gherkin
Dado que há duas doses vencidas entre os pets presentes
Quando abro o Painel do dia
Então o aviso do topo distingue quantas estão atrasadas, não só pendentes
```

**CA3 — confirmação tardia registra o atraso**
```gherkin
Dado que a dose das 14:00 é confirmada às 14:27
Quando concluo a tarefa
Então o registro guarda o horário previsto e o horário real
E a tarefa consta como administrada com atraso
```

**CA4 — sem atraso, sem ruído**
```gherkin
Dado que nenhuma dose passou do horário
Quando abro o Painel do dia
Então nenhum destaque de atraso é exibido
```

### Notas técnicas
- A partir de quanto tempo a dose conta como atrasada depende da tolerância da
  **pergunta em aberto #8** — é o mesmo número que define a métrica 1. Enquanto não for
  decidido, o CA1 assume que atrasa no minuto seguinte ao horário previsto.
- O par horário previsto / horário real do CA3 é o dado que alimenta a métrica 1.
