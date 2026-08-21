# design/ — Especificações para o Claude Design

Esta pasta reúne as especificações de design do protótipo funcional da **primeira
fatia** do CãoMetria (o "Painel de Triagem do dia"), prontas para alimentar o
**Claude Design**.

## Arquivos

| Arquivo | O que é |
|---------|---------|
| [`sistema-visual.md`](sistema-visual.md) | Design tokens: cores, tipografia, forma, componentes e a lógica da cor de triagem. A fonte da verdade visual. |
| [`telas-primeira-fatia.md`](telas-primeira-fatia.md) | Spec tela a tela (5 telas / artboards): objetivo, layout, componentes e estados. |

## Como usar com o Claude Design

1. Abrir o Claude Design (skill `design`) para criar o canvas com os artboards.
2. Usar o `sistema-visual.md` como base de estilo (tokens) e o
   `telas-primeira-fatia.md` como roteiro dos artboards, na ordem sugerida.
3. Refinar visualmente no editor de canvas; exportar quando aprovado.

## Contexto

- **Visão do produto:** `../docs/visao-produto.md`
- **Apresentação (storytelling):** `../docs/apresentacao.html`
- **Prioridade de telas:** Painel do dia e Alerta de medicação — são as que melhor
  demonstram o diferencial (triagem visual + garantir que nada é esquecido).
