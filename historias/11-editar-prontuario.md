> Parte de **[CãoMetria — primeira fatia](historias-caometria-primeira-fatia.md)**.
> Contexto, escopo, premissas e perguntas em aberto estão no índice.

# História 11 — Editar o prontuário e trocar a coleira quando o risco muda

**Prioridade:** P1
**Depende de:** História 2

> **Como** atendente da creche
> **quero** alterar o prontuário de um pet já cadastrado
> **para que** um cão que começou a tomar remédio ou que teve um episódio de reatividade
> não fique com a informação — e a coleira — de meses atrás

### Critérios de aceite

**CA1 — alteração recalcula a coleira**
```gherkin
Dado que a Bila está cadastrada como verde
Quando edito o prontuário dela adicionando uma medicação com horário e salvo
Então a coleira dela passa a ser AMARELA em todas as telas
```

**CA2 — o risco mudou com o pet já na creche**
```gherkin
Dado que o pet já fez check-in hoje e está com a coleira VERDE
Quando altero o prontuário de forma que a cor derivada muda para VERMELHA
Então o app instrui explicitamente a trocar a coleira física do pet
E o painel passa a exibi-lo na nova cor e na nova posição de severidade
```

**CA3 — o que já aconteceu não se apaga**
```gherkin
Dado que uma dose de hoje já foi confirmada
Quando removo esse medicamento do prontuário
Então o medicamento deixa de gerar tarefas a partir de agora
E o registro da dose já administrada permanece no histórico do pet
```

**CA4 — nova medicação passa a alertar**
```gherkin
Dado que são 10:00 e o pet está presente
Quando adiciono uma medicação com dose às 16:00
Então o alerta das 16:00 passa a valer para hoje
```
> Comportamento para horário **já vencido** no momento do cadastro: pergunta em aberto #5.

**CA5 — cancelar não altera nada**
```gherkin
Dado que alterei campos na edição
Quando saio sem salvar
Então o prontuário permanece como estava
```

**CA6 — pet que deixou a creche**
```gherkin
Dado que um pet não frequenta mais a creche
Quando o marco como inativo
Então ele continua na lista de pets, exibido em cinza, indicando que o cadastro existe
E não aparece na lista de check-in enquanto estiver inativo
E o histórico dele permanece consultável
```

### Notas técnicas
- O protótipo não tem uma lista de todos os pets — a única listagem completa é a de
  check-in (`renderCheckin()`, que filtra os ausentes). O CA6 assume que essa listagem
  passa a distinguir três estados: ausente hoje, presente e inativo.
- "Não aparece no check-in enquanto inativo" é regra derivada, não dita: se a creche
  quiser reativar o pet direto pela tela de chegada, o critério muda.
