> Parte de **[CãoMetria — primeira fatia](historias-caometria-primeira-fatia.md)**.
> Contexto, escopo, premissas e perguntas em aberto estão no índice.

# História 9 — Bloquear a saída enquanto houver cuidado pendente

**Prioridade:** P0
**Depende de:** História 8

> **Como** atendente da creche
> **quero** ser impedido de fechar a saída com tarefa em aberto
> **para que** o cão não vá embora com o remédio do dia por administrar sem que ninguém
> tome uma decisão sobre isso

### Critérios de aceite

**CA1 — bloqueio com a pendência à vista**
```gherkin
Dado que a Nina tem a dose das 14:00 pendente
Quando tento concluir o check-out dela
Então a conclusão é bloqueada
E vejo quais tarefas estão pendentes, com horário e tipo
```

**CA2 — resolver a pendência no ato**
```gherkin
Dado que estou bloqueado pela dose pendente da Nina
Quando confirmo a dose ali mesmo, na tela de check-out
Então a pendência some
E o check-out pode ser concluído normalmente
```

**CA3 — registrar que o cuidado falhou**
```gherkin
Dado que a dose realmente não foi administrada e quem veio buscar o pet está no balcão
Quando registro a tarefa como "não administrada" e informo o motivo
Então o app exibe o aviso que preciso passar a quem está retirando o pet
E ao confirmar que avisei, o check-out é liberado
E a falha fica registrada no histórico do pet como cuidado não realizado, não como concluído
```

**CA4 — a falha não se esconde**
```gherkin
Dado que uma dose foi registrada como não administrada ontem
Quando abro o prontuário do pet
Então essa ocorrência está visível no histórico, com data, motivo e a informação de que o tutor foi avisado
```

### Notas técnicas
- O aviso ao tutor é presencial (premissa **P5**): o app registra a ciência, não envia
  nada. Se um dia for preciso notificar à distância, isso depende do portal do tutor, que
  está fora do escopo.
- Não confundir com o CA3 da História 6: lá é desfazer uma marcação errada; aqui é
  assumir que o cuidado não aconteceu.
