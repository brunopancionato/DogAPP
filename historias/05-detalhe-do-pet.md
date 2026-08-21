> Parte de **[CãoMetria — primeira fatia](historias-caometria-primeira-fatia.md)**.
> Contexto, escopo, premissas e perguntas em aberto estão no índice.

# História 5 — Abrir o prontuário do pet e falar com o tutor

**Prioridade:** P0
**Depende de:** História 3

> **Como** atendente da creche
> **quero** abrir o pet e ver o prontuário completo com os contatos
> **para que** eu consiga conferir o cuidado certo e ligar para o tutor quando algo foge
> do normal

### Critérios de aceite

**CA1 — prontuário completo**
```gherkin
Dado que abro o card de um pet presente
Quando a tela de detalhe carrega
Então vejo a cor da coleira, as tarefas de hoje, e os blocos de dieta, medicação e comportamento
E vejo a lista de tutores com a relação de cada um
```

**CA2 — reatividade em destaque permanente**
```gherkin
Dado que o Thor é reativo
Quando abro o detalhe dele
Então o aviso de isolamento e manejo aparece no topo, antes de qualquer outra informação
```

**CA3 — ligar para o tutor**
```gherkin
Dado que estou no detalhe de um pet
Quando toco no botão de ligar de um tutor
Então o discador do celular abre com o número dele
```

**CA4 — contato de emergência identificado**
```gherkin
Dado que um pet tem dois tutores cadastrados
Quando vejo a lista de contatos
Então o contato de emergência está marcado como tal
```

**CA5 — pet sem apontamentos**
```gherkin
Dado que a Bila é verde e não tem tarefas hoje
Quando abro o detalhe dela
Então vejo explicitamente que não há tarefa agendada e que não há apontamentos de comportamento
```
