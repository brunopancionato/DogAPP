# Briefing para colar no Claude Design — CãoMetria (primeira fatia)

> Cole este texto no Claude Design (claude.ai/design). É o roteiro completo do
> protótipo mobile clicável da primeira fatia. Detalhes de tokens e estados em
> `sistema-visual.md` e `telas-primeira-fatia.md`.

---

Crie um **protótipo mobile clicável** de um app de gestão de creche de cães chamado
**CãoMetria** — "cuidado sob medida para cães". Usuário: o **cuidador** no chão da
creche. Conceito central: **triagem de pronto-socorro** — cada pet tem uma coleira
colorida (🟢 verde = sem apontamentos · 🟡 amarela = dieta/remédio/alergia · 🔴
vermelha = reativo/agressivo). A cor é **derivada do prontuário** (maior severidade
manda). Mantenha **todas as ações clicáveis** e a navegação entre telas.

## Sistema visual
- **Marca (teal):** #0B5D5D — botões, links, seleção, ênfase.
- **Triagem (cores semânticas, só em contexto de risco):** verde #2E9E5B, amarelo
  #C98A0E, vermelho #CE4141 (fundos suaves: #E6F4EC / #FBF1DD / #FBE9E9).
- **Neutros:** fundo #F4F4F0 · cards #FFFFFF · texto #191B1F / #565A61 / #9A9EA4 ·
  linhas #E4E4DE.
- **Tipografia:** sans de sistema (títulos 700–800, tracking apertado); mono para
  horários/contadores. Sem emoji como ícone — use ícones SVG traçados.
- **Forma:** cards raio 16px, campos/botões 12px, badges pílula, avatar círculo.
  Alvo de toque ≥ 44px. Sombra sutil.

## Menu inferior flutuante (em todas as telas principais)
Barra que **flutua** (margem lateral e do rodapé), com 3 ações:
- **Esquerda:** ícone `+` "Novo" → abre Cadastro do pet.
- **Centro (destacado/elevado, círculo teal):** ícone casa "Hoje" → Painel do dia.
- **Direita:** ícone de entrada "Check-in" → fluxo de Check-in.

## Telas (5 artboards)

**1. Painel do dia (home):** header "Hoje" + data/contador; filtro por cor (Todos/🟢/🟡/🔴
com contagem); faixa de atenção no topo se houver tarefa vencendo; lista de cards de pet
(borda esquerda 4px na cor da coleira, avatar, nome, subtítulo de apontamentos, badge de
cor, relógio da próxima tarefa) — vermelhos no topo. Dados: Bila 🟢, Nina 🟡 (remédio
14:00 · ração sem grãos), Thor 🔴 (reativo · isolar). Menu inferior com "Hoje" ativo.

**2. Detalhe do pet:** cabeçalho com avatar grande, nome, raça/idade e puck da coleira;
faixa vermelha de reatividade se aplicável ("⚠️ isolar · manejo com cautela");
tarefas de hoje (chips 🍽️/💊 com horário e botão concluir — concluída mostra "✓ 12:03 ·
por Ana"); blocos colapsáveis de Dieta, Medicação, Comportamento e **Tutores (vários —
guarda compartilhada)** com botão de ligar; botão "Editar prontuário".

**3. Cadastro do pet:** formulário em seções — dados básicos (foto, nome, raça, idade,
porte); **Tutores repetível** ("+ Adicionar tutor"); Dieta (toggle → campos); Medicação
repetível (nome, dose, **horários** — o que dispara o alerta); Comportamento (toggle
"reativo" → observações). **Preview da coleira derivada em tempo real** ("Coleira
prevista: 🟡 AMARELA") conforme os toggles. Botão "Salvar prontuário".

**4. Check-in:** passo 1 selecionar pet que chegou (busca/lista); passo 2 tela grande de
instrução — puck enorme na cor derivada + "**Coloque a coleira AMARELA no Thor**" +
resumo dos apontamentos (se vermelho, reforço de isolamento) + botão "Confirmar
presença"; confirmação volta ao painel com o pet listado.

**5. Alerta de medicação (2 estados — requisito):** (A) notificação no celular:
💊 "Hora do remédio — Nina · Apoquel 5mg · 14:00", ações "Confirmar"/"Adiar". (B) tela
in-app: card de alerta crítico (fundo vermelho suave), medicamento/dose/horário, botões
**Confirmar dose** (registra quem/quando) e **Adiar 5 min**. Mostrar também o **caminho
de falha**: se passar do horário sem confirmar, o alerta re-dispara e o card do pet no
painel escala (estado "Dose atrasada · 14:12" em âmbar/vermelho).

Priorize o acabamento das telas **1 (Painel)** e **5 (Alerta)** — são as que melhor
demonstram o diferencial.
