> Parte de **[CãoMetria — primeira fatia](historias-caometria-primeira-fatia.md)**.
> Contexto, escopo, premissas e perguntas em aberto estão no índice.

# História 6 — Concluir uma tarefa de cuidado com comprovação

**Prioridade:** P0
**Depende de:** História 5

> **Como** atendente da creche
> **quero** marcar a comida e o remédio como feitos e ver registrado quando foi
> **para que** exista prova de que o cuidado aconteceu, em vez de memória de quem estava
> no turno

### Critérios de aceite

**CA1 — concluir alimentação**
```gherkin
Dado que a Nina tem alimentação agendada para 12:00
Quando marco a tarefa como concluída às 12:03
Então a tarefa passa a exibir "✓ 12:03" com a identificação da conta da creche
E deixa de contar como pendente no painel
```

**CA2 — concluir dose de medicamento**
```gherkin
Dado que a Nina tem Apoquel 5mg agendado para 14:00
Quando confirmo a dose
Então o horário real da confirmação fica registrado junto ao medicamento
E o aviso de medicação pendente do painel deixa de contá-la
```

**CA3 — desfazer uma marcação errada**
```gherkin
Dado que marquei por engano uma tarefa como concluída
Quando desmarco a tarefa
Então ela volta a constar como pendente
E o registro de que ela foi marcada e desmarcada permanece no histórico do pet
```

**CA4 — pet que não está na creche**
```gherkin
Dado que a Mel tem medicação agendada e não fez check-in hoje
Quando abro o prontuário dela
Então as tarefas de hoje aparecem como não aplicáveis
E não é possível concluí-las
```

**CA5 — dois aparelhos confirmam a mesma dose**
```gherkin
Dado que a dose das 14:00 da Nina já foi confirmada em outro aparelho às 14:02
Quando confirmo a mesma dose neste aparelho às 14:03
Então o registro das 14:02 é o que vale
E sou informado de que a dose já havia sido registrada, sem que um segundo registro seja criado
```

### Notas técnicas
- CA4 vem da premissa **P4**: o alerta do protótipo só considera pets presentes. Se a
  creche quiser registrar cuidado de pet ausente, a premissa cai e a história muda.
- O "quem" da comprovação é a conta da creche enquanto valer a premissa **P1** — no
  protótipo, `assinatura()` retorna a conta `CRECHE` ("Creche Patas Felizes"), que assina
  cada confirmação. A identificação por funcionário é do Horizonte 2.

### Fora desta história
- Foto ou observação anexada à conclusão da tarefa.
