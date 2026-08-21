# Histórias de Usuário — CãoMetria, primeira fatia (Painel de Triagem do dia)

| | |
|---|---|
| **Autor** | Bruno — a partir de entrevista de descoberta |
| **Data** | 19/08/2026 |
| **Status** | Em validação |
| **Fontes** | `prototipo/index.html` (protótipo funcional), `docs/visao-produto.md`, `design/telas-primeira-fatia.md` |

## Contexto

**Problema:** uma creche recebe dezenas de cães por dia com poucos cuidadores, e as
necessidades individuais estão espalhadas ao longo do dia — dieta específica, medicação
em horário determinado, cão reativo que precisa ficar isolado. Hoje isso depende de
alguém lembrar. Um remédio esquecido, a comida errada ou um cão reativo no grupo errado
não são falhas de processo: são incidentes que machucam o animal ou a equipe e quebram a
confiança do tutor.

**Usuário-alvo:** a **pessoa do atendimento** da creche. Neste momento existe **um único
celular, no balcão do atendimento**, e essa pessoa centraliza: recebe os alertas,
registra o que foi feito e avisa verbalmente os cuidadores que estão no chão. Ela não é
quem administra o remédio — é quem garante que alguém administrou.

**Métrica de sucesso:** duas, ambas sobre a promessa central ("nada é esquecido"):

1. **% de doses administradas no horário devido** — confirmações dentro da tolerância
   combinada, sobre o total de doses agendadas para pets presentes. Mede se a ferramenta
   cumpre o que promete. *A tolerância ainda não está definida — pergunta em aberto #8.*
2. **Adiamentos por alerta disparado** — total de "Adiar 5 min" dividido pelo total de
   alertas emitidos. É a métrica de atrito: se subir, o alarme está tocando na hora
   errada ou está sendo tratado como incômodo em vez de tarefa.

> Os dados das duas ficam registrados pelas histórias 6, 7 e 10 (horário previsto,
> horário real, cada disparo e cada adiamento). **O painel de indicadores está fora do
> escopo desta fatia** — nos primeiros 30 dias a leitura é por extração manual dos
> registros.

## Escopo

**Dentro** — todos os itens abaixo já estão implementados no protótipo funcional
(`prototipo/index.html`):

- [x] Acesso ao app com a conta da creche
- [x] Cadastro do prontuário do pet, com a cor da coleira **derivada** do que se preenche
- [x] Alergia como campo do prontuário (pinta a coleira em amarelo)
- [x] Edição do prontuário, com recálculo da coleira e aviso para trocar a coleira física
- [x] Check-in do dia com instrução da coleira física
- [x] Painel do dia: presentes, ordenados por severidade, filtro por cor
- [x] Detalhe do pet: prontuário e contato dos tutores
- [x] Concluir tarefa de cuidado (comida e remédio) com comprovação de quem e quando
- [x] Alerta de medicação **com o app fechado**, repetindo a cada 5 minutos até a
      conclusão *(demonstrado no protótipo com relógio e alarme simulados; o disparo real
      com o app fechado depende do alarme local do aparelho — premissa P3)*
- [x] Dose atrasada visível e escalada no painel
- [x] Check-out com registro de **quem levou o pet**
- [x] Retirada por terceiro, com autorização de um tutor cadastrado
- [x] Bloqueio do check-out enquanto houver tarefa pendente
- [x] Virada do dia, mantendo em aberto quem não teve check-out registrado
- [x] Pet desligado da creche continua na lista, acinzentado, como cadastro existente

**Fora (explicitamente):**

- [ ] **Perfil de funcionário vinculado à creche** — decisão de 19/08/2026: fica para
      depois. Consequência assumida na premissa P1
- [ ] Portal ou app do tutor
- [ ] Reserva, agenda comercial, cobrança e pagamentos
- [ ] Relatórios gerenciais e indicadores (a "metria" do nome)
- [ ] Registro de incidentes e ocorrências
- [ ] Vacinas, banho & tosa, adestramento, multi-unidade
- [ ] Versão web
- [ ] Foto do pet e campo de porte *(existem na spec de design, não no protótipo, e não
      foram incluídos nesta fatia)*

## Premissas

> Assumido, não verificado. Se alguma cair, as histórias mudam.

- **P1 — A comprovação assina com a conta da creche, não com uma pessoa.** Foi a decisão
  tomada (login único do estabelecimento; funcionários vinculados ficam para o futuro).
  Consequência que precisa ficar dita em voz alta: enquanto isso, "quem administrou"
  identifica o **estabelecimento**, não o indivíduo. A promessa de responsabilização
  individual da visão de produto só se cumpre no Horizonte 2.
- **P2 — Hoje há um único dispositivo por creche**, no balcão do atendimento. A regra de
  concorrência já está decidida para quando isso mudar: **vale o primeiro registro**
  (ver CA5 da História 6). O que não está decidido é se o segundo aparelho vê o registro
  do primeiro em tempo real, o que depende de haver servidor — decisão do tech lead.
- **P3 — O alerta é um alarme local agendado no aparelho**, não um push de servidor. É o
  que atende "tocar com o app fechado" sem exigir backend. Ver notas técnicas da
  História 7 — a decisão final é do tech lead.
- **P4 — Tarefas só valem para pets presentes.** Derivado do protótipo: `fireAlert()` só
  varre pets com `present:true`. Um pet que não fez check-in não gera alerta nem tarefa
  concluível no dia.
- **P5 — Decidido (não é mais premissa):** o aviso sobre uma dose não administrada é
  **presencial, no check-out**. O app exibe o alerta para quem está no balcão informar a
  quem veio buscar o pet, e registra que o aviso foi dado. Nada é enviado por nenhum
  canal — isso só existirá quando houver canal do tutor, no Horizonte 2.

## Perguntas em aberto

> A numeração é estável: pergunta respondida sai desta tabela e desce para as decididas,
> sem renumerar as demais — as referências espalhadas pelas histórias continuam válidas.

| # | Pergunta | Quem responde | Bloqueia? |
|---|---|---|---|
| 3 | Como a creche recupera o acesso se perder a senha da conta única? Não há e-mail de funcionário no escopo | Bruno | Não — mas trava a creche no dia em que acontecer |
| 4 | Ao resolver um "check-out não registrado" do dia anterior, o pet foi retirado sem baixa ou permaneceu na creche? A segunda hipótese abre pernoite, que está fora do escopo | Bruno / operação | Não — afeta o CA3 da História 12 |
| 5 | Medicação cadastrada no meio do dia com horário **já vencido**: dispara alerta retroativo ou só vale a partir de amanhã? | Bruno | Não — afeta o CA4 da História 11 |
| 6 | Com dezenas de pets, a lista de check-in precisa de busca por nome. Entra nesta fatia ou espera? | Bruno | Não |
| 7 | Quem autoriza a retirada por terceiro pode ser qualquer tutor do pet, ou só o contato de emergência? | Bruno / operação | Não — refina o CA4 da História 8 |
| 8 | Qual a tolerância para uma dose contar como "no horário"? (5, 10, 15 minutos após o previsto) | Bruno / veterinário de referência | Não — mas sem ela a métrica 1 não fecha, e o CA1 da História 10 fica vago |
| 9 | Se a Apple não conceder o *entitlement* de Critical Alert, o iOS entrega uma promessa mais fraca que o Android (o silencioso vence o alarme). Lança assim, lança só Android primeiro, ou espera? | Bruno | Não — mas define a plataforma da primeira entrega |

### Decididas em 19/08/2026

| Pergunta | Resposta |
|---|---|
| Métrica de sucesso | % de doses no horário devido, e adiamentos por alerta disparado — ver Contexto |
| Alarme no modo silencioso | **Tem que furar o silencioso.** Vale para as duas plataformas como intenção; a viabilidade real difere — ver História 7, CA7 e notas técnicas |
| Terceiro não cadastrado buscando o pet | Só se registra a retirada em nome de um tutor **já cadastrado**. Se for outra pessoa, é preciso contato para autorizar a saída, e o check-out registra que um terceiro veio buscar — História 8, CA3 a CA5 |
| Frequência e limite do alerta | Repete a cada 5 minutos; **adiar só é permitido duas vezes** — História 7, CA3, CA5 e CA6 |
| Canal do aviso de dose não administrada | Presencial, no check-out; canal do tutor fica para o futuro — premissa P5 e História 9 |
| Dois aparelhos confirmando a mesma dose | Vale o primeiro registro — História 6, CA5 |
| Pet que deixa a creche | Continua na lista, acinzentado, como cadastro existente — História 11, CA6 |

---

## As histórias

Uma história por arquivo. Prioridade é sugestão a validar com quem vai construir.

| # | História | Prio | Depende de |
|---|---|:---:|---|
| 1 | [Entrar no app com a conta da creche](01-login-conta-creche.md) | P0 | — |
| 2 | [Cadastrar o prontuário do pet e ver a coleira derivada](02-cadastro-prontuario.md) | P0 | — |
| 3 | [Registrar a chegada do pet e receber a instrução da coleira](03-check-in-coleira.md) | P0 | 2 |
| 4 | [Ver o painel do dia com a segurança no topo](04-painel-do-dia.md) | P0 | 3 |
| 5 | [Abrir o prontuário do pet e falar com o tutor](05-detalhe-do-pet.md) | P0 | 3 |
| 6 | [Concluir uma tarefa de cuidado com comprovação](06-concluir-tarefa.md) | P0 | 5 |
| 7 | [Ser alertado no horário da dose, mesmo com o app fechado](07-alerta-medicacao.md) | P0 | 3 |
| 8 | [Registrar a saída do pet e quem o levou](08-check-out-retirada.md) | P0 | 3 |
| 9 | [Bloquear a saída enquanto houver cuidado pendente](09-bloqueio-check-out.md) | P0 | 8 |
| 10 | [Ver a dose atrasada escalar no painel](10-dose-atrasada.md) | P1 | 7 |
| 11 | [Editar o prontuário e trocar a coleira quando o risco muda](11-editar-prontuario.md) | P1 | 2 |
| 12 | [Virar o dia sem perder quem ficou em aberto](12-virada-do-dia.md) | P1 | 8 |

## Ordem sugerida de entrega

> Sugestão a validar com quem vai construir — prioridade é conversa, não decreto.

1. **Fundação operável (P0):** 1 → 2 → 3 → 4 → 5 → 6. No fim desse bloco a creche já
   cadastra, faz check-in com a coleira certa, vê o painel e comprova cuidado. É a menor
   versão que entrega valor.
2. **A promessa do produto (P0):** 7 → 8 → 9. O alarme que insiste e a saída que não
   acontece com pendência. É aqui que a ferramenta deixa de ser lista passiva.
3. **Fechamento do ciclo (P1):** 10 → 11 → 12. Atraso visível, prontuário vivo e o dia
   que termina de verdade.
