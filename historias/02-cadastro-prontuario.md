> Parte de **[CãoMetria — primeira fatia](historias-caometria-primeira-fatia.md)**.
> Contexto, escopo, premissas e perguntas em aberto estão no índice.

# História 2 — Cadastrar o prontuário do pet e ver a coleira derivada

**Prioridade:** P0

> **Como** atendente da creche
> **quero** cadastrar o pet com dieta, medicação, alergia, reatividade e seus tutores
> **para que** o sistema saiba sozinho qual coleira o cão usa e quais cuidados ele exige,
> sem depender de alguém decidir a cor na mão

### Critérios de aceite

**CA1 — cadastro mínimo gera coleira verde**
```gherkin
Dado que estou no cadastro de um novo pet
Quando preencho nome e um tutor com nome e telefone, sem nenhum apontamento de cuidado
E salvo o prontuário
Então o pet é criado com a coleira VERDE
E aparece na lista de check-in como ausente
```

**CA2 — apontamento de cuidado gera coleira amarela**
```gherkin
Dado que estou cadastrando um pet
Quando ligo "dieta específica" e informo ração, porção e dois horários de refeição
Então o preview da coleira muda para AMARELA imediatamente, antes de salvar
E ao salvar, o pet passa a ter duas tarefas de alimentação por dia
```

**CA3 — reatividade vence a severidade**
```gherkin
Dado que estou cadastrando um pet com medicação já informada, com preview AMARELO
Quando ligo "reativo / agressivo"
Então o preview muda para VERMELHA
E ao salvar, o prontuário continua exibindo o apontamento de medicação
```

**CA4 — alergia sozinha já gera coleira amarela**
```gherkin
Dado que estou cadastrando um pet sem dieta e sem medicação
Quando informo uma alergia
Então o preview da coleira muda para AMARELA
E a alergia aparece em destaque no prontuário do pet
```

**CA5 — o app não inventa dado que faltou**
```gherkin
Dado que deixei o nome do pet em branco
Quando toco em "Salvar prontuário"
Então o cadastro não é salvo
E o campo obrigatório é destacado com a indicação do que falta
```

**CA6 — apontamento ligado exige o detalhe**
```gherkin
Dado que liguei "medicação" e não informei o nome do medicamento nem a dose
Quando toco em "Salvar prontuário"
Então o cadastro não é salvo
E os campos pendentes do bloco de medicação são destacados
```

**CA7 — vários tutores para o mesmo pet**
```gherkin
Dado que estou cadastrando um pet em guarda compartilhada
Quando adiciono um segundo tutor com nome, relação e telefone
Então os dois ficam salvos como contatos do pet
E o primeiro é identificado como contato de emergência
```

### Notas técnicas
- Resolvido: `validarForm()` bloqueia o salvamento com campos obrigatórios vazios (nome,
  ao menos um tutor com telefone, ração quando há dieta, medicamento e dose quando há
  medicação) e mostra o erro no próprio campo — o app não inventa mais o dado que faltou
  (CA5 e CA6). Prontuário com dado inventado é pior que prontuário vazio.
- A regra de cor é uma só, usada em cadastro, check-in, painel e detalhe (`corDoPet()`).

### Fora desta história
- Foto do pet e campo de porte.
- Editar o que foi cadastrado — História 11.
