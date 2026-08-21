> Parte de **[CãoMetria — primeira fatia](historias-caometria-primeira-fatia.md)**.
> Contexto, escopo, premissas e perguntas em aberto estão no índice.

# História 4 — Ver o painel do dia com a segurança no topo

**Prioridade:** P0
**Depende de:** História 3

> **Como** atendente da creche
> **quero** ver num relance quem está na creche hoje e o que exige atenção
> **para que** eu saiba a quem avisar primeiro, sem abrir pet por pet

### Critérios de aceite

**CA1 — ordem por severidade**
```gherkin
Dado que há pets vermelhos, amarelos e verdes presentes
Quando abro o Painel do dia
Então os vermelhos aparecem primeiro, depois os amarelos, depois os verdes
E dentro da mesma cor, quem tem a próxima tarefa mais cedo aparece antes
```

**CA2 — o card resume o pet**
```gherkin
Dado que a Nina está presente com remédio às 14:00
Quando vejo o card dela no painel
Então vejo o nome, a cor da coleira, o resumo dos apontamentos e o horário da próxima tarefa
```

**CA3 — filtro por cor**
```gherkin
Dado que estou no Painel do dia
Quando aplico o filtro VERMELHO
Então vejo apenas os pets reativos presentes
E o contador do filtro mostra quantos são
```

**CA4 — filtro sem resultado**
```gherkin
Dado que nenhum pet vermelho está presente hoje
Quando aplico o filtro VERMELHO
Então vejo a mensagem de que nenhum pet se encaixa nesse filtro
```

**CA5 — creche ainda vazia**
```gherkin
Dado que nenhum pet fez check-in hoje
Quando abro o Painel do dia
Então vejo o estado vazio indicando que ninguém chegou ainda
E o caminho para o check-in fica à mão
```

**CA6 — aviso de medicação pendente**
```gherkin
Dado que há doses pendentes entre os pets presentes
Quando abro o Painel do dia
Então vejo no topo quantas medicações estão pendentes hoje
E tocar nesse aviso me leva à dose mais próxima
```
