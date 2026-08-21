# CãoMetria — Telas da Primeira Fatia

Especificação das telas do protótipo funcional: **o "Painel de Triagem do dia".**
Cada tela é um artboard para o Claude Design. Segue o `sistema-visual.md`.

- **Usuário primário:** a **pessoa do atendimento**. Na 1ª fatia a creche tem **um
  aparelho, no balcão** (premissa P2 das histórias) — quem o opera não administra o
  remédio, **garante que alguém administrou**. O cuidador no chão é beneficiário:
  recebe a informação pela **coleira física** e pelo aviso da recepção. App próprio
  para ele é o primeiro item do Horizonte 2.
- **Dispositivo:** mobile. Desenhado para o bolso desde já, porque é para lá que vai —
  e porque o alarme precisa tocar com o app fechado (premissa P3).
- **Fluxo geral:** Cadastro → Check-in → Painel do dia → Detalhe/tarefas →
  Alerta de medicação → Check-out (com bloqueio por pendência).

### Elemento global — Menu inferior flutuante
Todas as telas principais (Painel, Detalhe, e telas de retorno) exibem o **menu
inferior flutuante** definido no `sistema-visual.md`. Três ações:

- **Esquerda `+`** → Novo cliente / Cadastro do pet (Tela 3)
- **Centro (elevado) 🏠** → Home / Painel do dia (Tela 1) — a âncora
- **Direita ⇥** → Check-in (Tela 4)

Reservar ~80px de respiro no rodapé do conteúdo para a barra não cobrir itens.
Telas de fluxo em foco (formulário de cadastro, passos do check-in, alerta modal)
podem ocultar a barra para não competir com a ação principal.

Ordem sugerida dos artboards (da esquerda para a direita no canvas):

```
1. Painel do dia   2. Detalhe do pet   3. Cadastro do pet
4. Check-in        5. Alerta de medicação (2 estados)   6. Check-out & bloqueio
```

---

## Tela 1 — Painel do dia  *(home)*

**Objetivo:** o cuidador abre o app e vê, num relance, quais pets estão presentes
hoje e o que exige atenção — por cor.

**Layout (mobile, topo → base):**
- **Header:** "Hoje" grande + data e contador ("14:00 · 12 pets presentes").
  Ícone de perfil/menu à direita.
- **Barra de filtro por cor:** chips "Todos · 🟢 · 🟡 · 🔴" (com contagem em cada).
  Padrão: ordenar vermelhos no topo (segurança primeiro).
- **Faixa de atenção (se houver tarefa vencendo):** um card fino teal/amarelo no topo
  — "1 medicação nos próximos 15 min" → leva à tarefa.
- **Lista de pets:** cards de pet (ver componente), ordenados por severidade e depois
  por próxima tarefa. Cada card:
  - borda esquerda 4px na cor da coleira;
  - avatar + nome + subtítulo (ex.: "remédio 14:00 · ração sem grãos" / "reativo ·
    isolar" / "sem apontamentos");
  - badge de cor à direita; se pendente, relógio com horário da próxima tarefa.
- **Menu inferior flutuante:** presente (home ativa no centro). Substitui o FAB
  isolado — check-in e novo cliente ficam nas laterais da barra.

**Estados:** lista cheia; filtro vermelho aplicado (só reativos); vazio ("nenhum pet
presente ainda hoje").

---

## Tela 2 — Detalhe do pet

**Objetivo:** ver o prontuário resumido e executar/comprovar as tarefas do dia.

**Layout:**
- **Cabeçalho do pet:** avatar grande, nome, raça/idade, e o **puck** da coleira com
  o rótulo ("Coleira vermelha · reativo").
- **Faixa de reatividade (se vermelho):** banner `red-tint` fixo — "⚠️ Reativo —
  isolar do grupo. Manejo com cautela." (protege pet, outros cães e equipe).
- **Tarefas de hoje:** lista de chips de tarefa (🍽️ comida, 💊 remédio) com horário
  e botão concluir. Concluídas mostram quem fez e quando ("✓ 12:03 · por Ana").
- **Prontuário (blocos colapsáveis):**
  - **Dieta:** ração/porção/horários, restrições, alergias.
  - **Medicação:** cada remédio com dose e horários.
  - **Comportamento:** notas de reatividade.
  - **Tutores (contatos):** lista — pode ter vários (ex.: guarda compartilhada);
    nome, relação, telefone, botão de ligar. Marcar contato de emergência.
- **Rodapé:** botão "Editar prontuário".

**Estados:** pet verde (sem faixa de reatividade, poucas tarefas); pet amarelo (tarefas
de comida/remédio); pet vermelho (faixa de alerta + possíveis tarefas amarelas juntas).

---

## Tela 3 — Cadastro do pet

**Objetivo:** criar o prontuário — a porta de entrada de todo o resto. A cor da
coleira é **derivada** do que se preenche, mostrada em preview em tempo real.

**Layout (formulário em seções):**
- **Dados básicos:** foto (upload), nome, raça, idade, porte.
- **Tutores (contatos):** repetível — "+ Adicionar tutor" (nome, relação, telefone).
  Suporta múltiplos (guarda compartilhada). Marcar "contato de emergência".
- **Dieta:** toggle "tem dieta específica" → campos de ração, porção, horários,
  restrições/alergias.
- **Medicação:** repetível — "+ Adicionar medicamento" (nome, dose, horários). Cada
  horário adicionado é o que dispara o alerta.
- **Comportamento:** toggle "reativo / agressivo" → campo de observações de manejo.
- **Preview da coleira (fixo no rodapé ou topo):** mostra a cor derivada em tempo
  real conforme os toggles: "Coleira prevista: 🟡 AMARELA". Deixa a regra visível.
- **Ação:** botão primário "Salvar prontuário".

**Estados:** vazio (novo); preenchido gerando amarelo; reativo marcado gerando
vermelho (preview muda na hora).

---

## Tela 4 — Check-in do dia

**Objetivo:** registrar a chegada do pet e instruir a coleira física — o momento em
que o digital vira físico.

**Fluxo (pode ser 1–2 telas / passos):**
1. **Selecionar pet que chegou:** busca/lista de pets cadastrados.
2. **Instrução da coleira:** tela de confirmação grande e inequívoca —
   - **puck** enorme na cor derivada + texto: **"Coloque a coleira AMARELA no Thor"**;
   - resumo dos apontamentos ("remédio 14:00 · ração sem grãos");
   - se vermelho: reforço de manejo/isolamento;
   - botão primário "Confirmar presença".
3. **Confirmação:** toast "Thor está presente" → volta ao painel com o pet já listado.

**Estados:** instrução verde / amarela / vermelha (a tela inteira ecoa a cor no puck e
no destaque, sem colorir demais o resto).

---

## Tela 5 — Alerta de medicação  *(o coração da fatia — 2 estados)*

**Objetivo:** garantir que a dose aconteça no horário e seja comprovada. É o coração
do "de lembrar para garantir".

**Estado A — Notificação (lock screen / push):**
- Notificação do sistema no aparelho da creche: ícone 💊, título **"Hora do remédio
  — Nina"**, corpo "Dose 14:00 · Apoquel 5mg". Ações rápidas: "Confirmar" / "Adiar".
- Mostrar como mockup de notificação sobre uma lock screen.

**Estado B — Tela de confirmação (in-app):**
- **Card de alerta crítico** (`red-tint`/`red`): 💊 + "Hora do remédio — Nina".
- Detalhe: medicamento, dose, horário previsto.
- **Comprovação:** ao confirmar, registra quando e sob qual conta (automático).
  Enquanto não houver perfil de funcionário, a assinatura é da **conta da creche**, não
  de um indivíduo — premissa P1, e é o que o Horizonte 2 corrige.
- Botões: **Confirmar dose** (primário) · **Adiar 5 min** (secundário).
- **Limite do adiamento:** duas vezes. Na terceira, o botão de adiar some e o texto
  passa a ser "Adiado 2 vezes — não é mais possível adiar. O alerta continua a cada
  5 min até a dose ser resolvida." Ilustrar esse terceiro estado.
- **Comportamento de falha (importante mostrar):** se o horário passa sem confirmação,
  o alerta **re-dispara** e o card do pet no painel **escala** (fica vermelho/pulsa) —
  incluir um mini-estado "Dose atrasada · 14:12" em `warning` para ilustrar o caminho
  de falha, não só o caminho feliz.

**Estados:** alerta ativo; dose confirmada (check verde "Administrado 14:03 · por
Ana"); dose atrasada (aviso âmbar/vermelho).

---

## Tela 6 — Check-out & bloqueio por pendência

**Objetivo:** fechar o ciclo. É a tela que entrega o verbo do case — *garantir* — e o
mecanismo que nenhuma ferramenta analisada tem: **o cão não sai com cuidado pendente.**

**Fluxo:**
1. **Quem está levando o pet:** lista dos tutores-contato cadastrados, com opção
   "outra pessoa". Se for terceiro, exige **autorização de um tutor cadastrado**, e o
   check-out registra que um terceiro veio buscar.
2. **Verificação de pendências:** se houver tarefa de cuidado não resolvida, a saída é
   **bloqueada** — banner de aviso listando o que falta, com atalho para resolver.
3. **Aviso de dose não administrada:** quando a dose não aconteceu, o app exibe o
   alerta para quem está no balcão **informar presencialmente** a quem veio buscar, e
   registra que o aviso foi dado. Nada é enviado por nenhum canal — canal do tutor é
   Horizonte 2 (premissa P5).
4. **Confirmação:** registra hora da saída e quem levou.

**Layout:**
- Cabeçalho do pet com o puck da coleira.
- **Banner de bloqueio** (`red-tint`): "Saída bloqueada — 1 cuidado pendente", com a
  lista das tarefas e o horário previsto de cada uma.
- Seleção de quem leva: cards de tutor; card "outra pessoa" abre o passo de autorização.
- Botão primário **"Confirmar saída"** — desabilitado enquanto houver pendência.

**Estados:** saída livre (sem pendência); **saída bloqueada** (o estado que importa);
retirada por terceiro aguardando autorização; dose não administrada com aviso a dar.

---

## Notas para o Claude Design

- **Reutilizar tokens** do `sistema-visual.md` — não inventar cores novas.
- **Dados realistas** (nomes: Bila 🟢, Nina 🟡, Thor 🔴; remédios reais; horários).
  Nunca "lorem ipsum".
- **Consistência de componentes** entre telas (o card de pet é o mesmo em todo lugar).
- **Uma coleira, uma verdade:** a mesma lógica de cor em cadastro, check-in, painel e
  detalhe.
- Priorizar as telas **1 (Painel)**, **5 (Alerta)** e **6 (Bloqueio da saída)** — são as
  três que demonstram o diferencial. O bloqueio é o clímax: é onde "lembrar" vira
  "garantir".
- **A coleira sinaliza, não atesta.** Nada na interface pode sugerir que o app declara
  um cão seguro — a cor espelha o que a creche registrou. Evitar rótulos como "seguro",
  "liberado" ou "ok para o grupo".
