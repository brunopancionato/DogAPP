> Parte de **[CãoMetria — primeira fatia](historias-caometria-primeira-fatia.md)**.
> Contexto, escopo, premissas e perguntas em aberto estão no índice.

# História 8 — Registrar a saída do pet e quem o levou

**Prioridade:** P0
**Depende de:** História 3

> **Como** atendente da creche
> **quero** registrar a retirada informando qual tutor levou o pet
> **para que** exista registro de que o cão saiu com a pessoa certa — e o painel de hoje
> reflita quem ainda está na creche

### Critérios de aceite

**CA1 — retirada por um tutor cadastrado**
```gherkin
Dado que a Nina está presente e o Carlos chegou para buscá-la
Quando registro o check-out selecionando o Carlos entre os tutores dela
Então a saída fica registrada com o nome dele e o horário
E a Nina deixa de aparecer no Painel do dia
```

**CA2 — guarda compartilhada**
```gherkin
Dado que a Nina tem dois tutores cadastrados
Quando abro o check-out dela
Então os dois aparecem como opção de quem está retirando
E o registro guarda qual dos dois levou o pet naquele dia
```

**CA3 — a retirada é sempre em nome de um tutor cadastrado**
```gherkin
Dado que estou registrando o check-out de um pet
Quando escolho quem está retirando
Então só posso selecionar tutores cadastrados no prontuário do pet
E não existe campo livre para digitar outra pessoa
```

**CA4 — terceiro veio buscar, com autorização**
```gherkin
Dado que quem chegou para buscar o pet não é contato cadastrado
Quando entro em contato com um tutor cadastrado e ele autoriza a saída
E registro o check-out em nome desse tutor, marcando que um terceiro veio buscar
Então a saída é concluída
E fica registrado no histórico do pet que a retirada foi feita por terceiro, com quem autorizou e o horário
```

**CA5 — sem autorização, sem saída**
```gherkin
Dado que quem chegou não é contato cadastrado e nenhum tutor autorizou
Quando tento concluir o check-out
Então a conclusão é bloqueada
E o app oferece o contato dos tutores do pet para eu ligar
```

**CA6 — pet sem pendência sai direto**
```gherkin
Dado que o pet não tem nenhuma tarefa pendente hoje
Quando registro o check-out
Então a saída é concluída sem nenhum passo adicional
```

**CA7 — só sai quem entrou**
```gherkin
Dado que um pet não fez check-in hoje
Quando abro a lista de check-out
Então ele não aparece como opção
```

### Notas técnicas
- O CA3 é o que fecha o furo de segurança: campo livre de texto voltaria a permitir
  entregar o cão para qualquer um, com registro bonito e inútil.
- Quem pode autorizar a retirada por terceiro — qualquer tutor ou só o contato de
  emergência — é a **pergunta em aberto #7**.

### Fora desta história
- Registrar nome ou documento do terceiro que retirou: o registro é de que houve
  terceiro e de quem autorizou.
- Assinatura eletrônica ou comprovante de retirada.
- Bloqueio por pendência — História 9.
