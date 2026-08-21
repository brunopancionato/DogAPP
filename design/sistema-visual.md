# CãoMetria — Sistema Visual

Especificação de design tokens para o protótipo da primeira fatia. Deriva da
identidade já validada na apresentação (`docs/apresentacao.html`). Serve de base
para todas as telas no Claude Design.

---

## 1. Princípios visuais

- **App de operação, não de leitura.** Telas são escaneadas e operadas por um
  cuidador em movimento — hierarquia clara, alvos de toque generosos, estado visível
  num relance.
- **A cor da triagem é semântica, não decorativa.** Verde / amarelo / vermelho
  *significam* algo (o risco do pet). Nunca usar essas cores para enfeite.
- **Teal é a marca.** Botões, links, seleção, ênfase — teal. Nunca confundir com a
  triagem.
- **Mobile-first.** O usuário primário é o cuidador com o celular no bolso; o alerta
  de medicação é uma exigência mobile.

---

## 2. Cores

### Marca
| Token | Hex | Uso |
|-------|-----|-----|
| `brand` | `#0B5D5D` | Ações primárias, links, seleção, ênfase |
| `brand-ink` | `#083F3F` | Texto sobre fundos claros de marca |
| `brand-tint` | `#E7F0F0` | Fundos suaves, avatares, chips |

### Triagem (semântica — só em contexto de risco)
| Token | Hex | Significado |
|-------|-----|-------------|
| `green` | `#2E9E5B` | Verde — sem apontamentos |
| `green-tint` | `#E6F4EC` | Fundo de badge verde |
| `amber` | `#C98A0E` | Amarela — cuidado (dieta / remédio / alergia) |
| `amber-tint` | `#FBF1DD` | Fundo de badge amarelo |
| `red` | `#CE4141` | Vermelha — reativo / agressivo |
| `red-tint` | `#FBE9E9` | Fundo de badge vermelho |

### Neutros (levíssimo viés quente)
| Token | Hex | Uso |
|-------|-----|-----|
| `paper` | `#F4F4F0` | Fundo da tela |
| `surface` | `#FFFFFF` | Cards, campos, barras |
| `surface-2` | `#FAFAF7` | Card aninhado / linha de lista |
| `ink` | `#191B1F` | Texto principal |
| `ink-soft` | `#565A61` | Texto secundário |
| `ink-faint` | `#9A9EA4` | Texto terciário / placeholder |
| `line` | `#E4E4DE` | Divisórias / bordas |

### Semânticos de sistema (separados da triagem)
| Token | Hex | Uso |
|-------|-----|-----|
| `success` | `#2E9E5B` | Tarefa concluída (coincide com green, ok) |
| `warning` | `#C98A0E` | Dose atrasada |
| `danger` | `#CE4141` | Erro / dose perdida |

> **Modo escuro** existe na apresentação, mas o protótipo pode ser entregue só em
> tema claro para simplificar. Se fizermos escuro, seguir os mesmos tokens
> invertidos do deck.

---

## 3. Tipografia

Fontes de sistema (sem webfont — robusto em qualquer dispositivo da creche).

| Papel | Família | Uso |
|-------|---------|-----|
| **Display / títulos** | `"Segoe UI", system-ui, -apple-system, Roboto, sans-serif`, peso 700–800, tracking apertado | Títulos de tela, nomes de pet |
| **Corpo** | mesma família, peso 400–600 | Textos, listas, campos |
| **Serifa (acento)** | `"Cambria", "Georgia", serif`, itálico | Somente momentos de marca (splash, vazio) — usar com parcimônia num app |
| **Mono / dados** | `"Consolas", ui-monospace, monospace` | Horários, contadores, labels de sistema |

### Escala (mobile)
- Título de tela: 24–28px / 800
- Nome do pet (card): 17px / 700
- Corpo: 15–16px / 400
- Secundário: 13–14px / 400, cor `ink-soft`
- Label/eyebrow: 11–12px / 600, uppercase, tracking `.08em`, mono

---

## 4. Forma e espaçamento

- **Grid base:** 8px. Paddings de tela: 20px laterais.
- **Raio:** cards 16px · campos/botões 12px · chips/badges 99px (pílula) · avatar 50%.
- **Sombra:** `0 1px 2px rgba(20,22,26,.04), 0 8px 24px rgba(20,22,26,.06)` — sutil.
- **Alvo de toque mínimo:** 44×44px.

---

## 5. Componentes-chave

### Coleira (indicador de triagem) — o componente assinatura
Aparece em todo card de pet. Duas formas:
- **Barra lateral:** borda esquerda de 4px na cor da triagem (no card do painel).
- **Puck:** círculo cheio na cor (no detalhe / check-in), com anel interno branco sutil.
- **Badge:** pílula com `*-tint` de fundo e texto na cor, rótulo em mono minúsculo
  (`verde` / `amarela` / `vermelha`).

### Card de pet (item do painel)
`[ avatar ] [ nome + subtítulo de apontamentos ] [ badge de cor ]`
com borda esquerda 4px = cor da triagem. Se houver tarefa pendente, mostrar um
pequeno contador/relógio à direita.

### Chip de tarefa
Linha com ícone (🍽️/💊), rótulo, horário (mono) e um botão-alvo de "concluir"
(círculo → check). Estado concluído: check verde + horário real riscado.

### Card de alerta de medicação (crítico)
Fundo `red-tint`, borda `red`, ícone 💊 em quadrado `red`, título forte, subtítulo
com a instrução, e dois botões: **Confirmar dose** (primário) e **Adiar 5 min**.

### Botões
- **Primário:** fundo `brand`, texto branco, raio 12px, altura 48px.
- **Secundário:** contorno `line`, texto `ink`.
- **Destrutivo/crítico:** fundo `red` (só em contexto de risco/erro).

### Menu inferior flutuante (navegação global) — presente em todas as telas principais
Barra flutuante fixa na base, para atuar de forma prática entre as opções sem sair da
tela. Não encosta nas bordas: "flutua" com margem lateral (~16px) e do rodapé (~14px),
raio grande (pílula/24px), fundo `surface`, sombra elevada, respeitando a safe-area.

Três ações, com a **home no centro em destaque**:

```
[  +  Novo cliente ]      (● HOJE ●)      [  ⇥  Check-in  ]
      esquerda           centro (home)          direita
```

- **Centro — Home (Hoje):** botão **elevado e maior**, círculo `brand` com ícone de
  casa (ou pata), levemente acima da barra (estilo "docked FAB"). Leva ao Painel do
  dia (Tela 1). É a âncora — o cuidador sempre volta pra cá.
- **Esquerda — Novo cliente:** ícone `+`, rótulo curto "Novo". Abre o Cadastro do pet
  (Tela 3).
- **Direita — Check-in:** ícone de entrada/chegada (⇥ / porta), rótulo "Check-in".
  Abre o fluxo de Check-in (Tela 4).

Estados: item ativo com ícone/rotulo em `brand`; inativos em `ink-soft`. Alvo de toque
≥ 44px. Ícones com rótulo curto embaixo (11px, mono ou sans).

> Substitui o antigo FAB isolado de check-in — a navegação principal passa a viver
> toda nesta barra.

### Campos de formulário
Fundo `surface`, borda `line` (foco = borda `brand` + halo), label acima em
`ink-soft` 13px. Erro em `danger` com mensagem que diz o que corrigir.

---

## 6. Regras da cor de triagem (lógica, não só estilo)

A cor **é derivada do prontuário**, não escolhida à mão:

```
se (reatividade == true)            -> VERMELHA
senão se (temMedicacao || temDieta || temAlergia) -> AMARELA
senão                                -> VERDE
```

- A cor exibida é sempre a **maior severidade** (vermelha > amarela > verde).
- O card/detalhe carrega **todos** os apontamentos, mesmo que a coleira seja vermelha
  (um pet vermelho pode também ter remédio → mostrar o chip de remédio no detalhe).
