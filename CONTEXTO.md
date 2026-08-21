# CãoMetria — Contexto e próximos passos

> **Para quem pegar este projeto do zero.** Escrito em 20/08/2026, ao fim de uma sessão de
> pesquisa de mercado + alinhamento dos artefatos. Leia isto antes de mexer em qualquer arquivo.

---

## 1. O que é isto

Case de entrevista para vaga de **Product Manager**. Não é produto real, não há cliente
para entrevistar, não há usuário para validar. Tudo que não estiver no enunciado é
**premissa assumida** — e assumir premissa em voz alta é parte do que está sendo avaliado.

**Prazo:** a conversa com o time é iminente (restavam menos de 24h quando este documento
foi escrito).

### O enunciado, literal

> **O contexto**
>
> Você ficou sabendo que uma creche para cachorros está precisando de um aplicativo para
> gerenciar os pets que a frequentam. Ela está com dificuldade em garantir que cada
> cachorro receba o cuidado adequado. Por exemplo:
>
> - Alguns pets têm dieta específica e precisam comer em horários determinados
> - Alguns pets precisam tomar medicação em horários determinados
> - Alguns pets têm problemas de reatividade e precisam ficar mais isolados dos outros
>
> **O que fazer antes da conversa**
>
> - Definir sua visão para o produto e a primeira fatia que priorizaria
> - Construir um protótipo dessa primeira fatia utilizando sua IA programadora favorita
>
> **O que esperamos na conversa**
>
> Durante a sessão, você vai apresentar sua visão do produto e o que construiu para o
> time, explicando seu racional, seu processo e mostrando como usou IA ao longo dele.
>
> Importante: não há um formato fixo de apresentação. Traga o que fizer sentido para
> comunicar sua visão e mostrar o que você construiu. Você terá 2 dias.

### As sete obrigações, e onde cada uma é atendida

| # | O que o case pede | Onde está |
|---|---|---|
| 1 | Visão do produto | `docs/visao-produto.md` §1 · deck slide "Visão" |
| 2 | Primeira fatia **priorizada** | `docs/visao-produto.md` §7 (com critério de corte) · deck slide "1ª fatia" |
| 3 | Protótipo dessa fatia, com IA | `prototipo/index.html` |
| 4 | Apresentar a visão | deck |
| 5 | Apresentar **o que construiu** | deck slide "1ª fatia" (10 itens) + demo ao vivo |
| 6 | Racional | deck slides Discovery → Métricas |
| 7 | **Como usou IA** | deck slide "Como usei IA" |

---

## 2. Os artefatos

```
D:\Projetos\Aplicativo para Doguinho\
├── CONTEXTO.md                      ← este arquivo
├── docs/
│   ├── apresentacao.html            ← DECK, 15 slides, HTML autocontido
│   ├── apresentacao.backup-20260820-152514.html
│   ├── visao-produto.md             ← documento-mãe
│   ├── visao-produto.backup-20260820-154900.md
│   └── anexo-analise-competitiva.md ← tabela comparativa completa + fontes (material de apoio)
├── design/
│   ├── telas-primeira-fatia.md      ← spec das 6 telas
│   ├── telas-primeira-fatia.backup-20260820-154900.md
│   ├── sistema-visual.md            ← tokens, não foi alterado
│   ├── brief-claude-design.md
│   └── README.md
├── historias/
│   ├── historias-caometria-primeira-fatia.md   ← índice, premissas, perguntas em aberto
│   └── 01…12-*.md                              ← uma história por arquivo
└── prototipo/
    ├── index.html                   ← PROTÓTIPO funcional, 1.374 linhas, sem dependências
    └── index-v1.html.bak            ← versão de 19/08 18:21 (anterior às mudanças de 20/08)
```

**O deck e o protótipo abrem direto no navegador.** Não há build, servidor, npm nem nada.

> ⚠️ Esta máquina **não tem Node nem Python**. Qualquer script de manipulação de arquivo
> precisa ser feito com as ferramentas de edição, não com interpretador.

---

## 3. A tese do produto, em uma página

**Nome de trabalho:** CãoMetria.

**Visão:** *Nenhum cuidado é esquecido. Toda creche opera com a segurança de um bom
pronto-socorro — e todo tutor confia que seu cão está bem cuidado.*

### Os três exemplos do case não são uma dor só

Este é o insight que organiza tudo:

| | Dieta + medicação | Reatividade |
|---|---|---|
| Natureza | **Tarefa** discreta, agendada, binária | **Estado** contínuo de manejo e espaço |
| Falha | Esquecimento, troca de turno | Julgamento sob pressão, espaço, ratio de pessoal |
| Tem "concluído"? | Sim, e é auditável | Não |
| Resolve com | Lista do turno + comprovação | Sinalização física + composição de grupo |

Daí a metáfora de **triagem de pronto-socorro**: 🟢 sem apontamentos · 🟡 **tarefa**
(comida/remédio/alergia) · 🔴 **estado** (reativo → isolar). A cor é **derivada do
prontuário**, não atribuída na mão, e o app instrui a coleira física no check-in.

### As três regras da coleira

1. A cor é **derivada** do prontuário — o app calcula e instrui.
2. A cor mostra a **maior severidade**; o card carrega todos os apontamentos.
3. **A cor não é um laudo de segurança** — ela espelha o que a creche registrou.
   Sinalizar ≠ atestar. *(Regra defensiva: atestar segurança é assumir responsabilidade
   civil por uma briga. Ver §4.)*

### Modelo pet-cêntrico

O mercado modela **dono → pets** (o pagador é a entidade central). Aqui é **pet →
tutores-contato**. Destrava guarda compartilhada, faz o cuidado ser cidadão de primeira
classe, e a operação do dia flui do pet.

---

## 4. A pesquisa de mercado — não refazer

> 📄 **A análise completa está em `docs/anexo-analise-competitiva.md`** — tabela comparativa
> com origem (nacional/internacional), segmento (dedicado × adaptável × referência), força
> da evidência por linha, a tabela do eixo comercial que sustenta o slide 8, e a lista de
> fontes. **Não é slide** — é o material que se abre quando alguém questiona a matriz.

Levantadas 12 ferramentas; **três investigadas a fundo** (documentação, tabela de planos,
changelog). Tudo abaixo foi acessado em **20/08/2026**.

### Fatos verificados, com fonte

| Achado | Fonte |
|---|---|
| Plano do Gingr para **creche** (Play, US$142/mês) **não lista** alimentação nem medicação entre os diferenciais; o de **hospedagem** (Stay, US$154) **lista** | [gingrapp.com/pricing](https://www.gingrapp.com/pricing) |
| Retrospectiva 2025 do Gingr: ano *"focused on driving recurring revenue"* — 4 entregas de receita × 2 operacionais | [Year in Review 2025](https://www.gingrapp.com/blog/year-in-review-a-2025-gingr-product-recap-for-pet-care-businesses) |
| Gingr agenda medicação por **janela** ("AM", "Lunch"), não por relógio | doc de Medication Schedule |
| Gingr cobra **automaticamente por administração de medicamento** | [Automated Medication Charges](https://support.gingrapp.com/hc/en-us/articles/29948509200013-Set-Up-Automated-Medication-Charges-Process) |
| Gingr: reatividade é **ícone + pop-up que dispara no balcão**, ao mexer na reserva | doc de Animal Icons / Pop Up Alerts |
| Gingr (set/2025): *booking restrictions based on evaluation results* — gating na porta, não manejo no pátio | release de setembro/2025 |
| **MoeGo**: alimentação e medicação com **horário de relógio**, dose, unidade, **atribuição a funcionário específico**, desfecho padronizado ("Took full dose on time") | [help.moego.pet](https://help.moego.pet/en/articles/14085065-how-to-apply-feeding-medication) |
| **MoeGo imprime** *activity cards* (checklist do dia por horário) e **collar labels** | [Print cards](https://help.moego.pet/en/articles/14085071-print-cards-for-boarding-daycare) |
| MoeGo tem artigo *"Feeding and medication fee (Beta)"* | referência cruzada na central (artigo não abriu) |
| Central de ajuda do MoeGo: **"Payments" = 44 artigos**, maior coleção, **> "Boarding & Daycare" (37)** | [help.moego.pet](https://help.moego.pet/en/) |
| **Sispet** (BR) se apresenta como **"Super Sistema ERP para Pet Shop…"**; creche é a 5ª de 9 seções; sem medicação estruturada | [sispet.com.br](https://sispet.com.br/) |
| **brightwheel** (creche **infantil**): registra dose e horário e **alerta quando a sala sai do ratio adulto/criança, em tempo real** | [mybrightwheel.com](https://mybrightwheel.com/blog/medication-administration-in-childcare-programs) |
| **"Ollie's Law"** (Massachusetts), vigente desde dez/2024: exige de creches caninas ratio, tamanho de grupo e **reporte obrigatório de lesão** | Animal Legal Defense Fund |
| Revelation Pets e DoggieDashboard **não fazem gating de cuidado por plano** — cuidado não é monetizado por tier | páginas de preço |

### O achado central

**Nenhum produto documenta regra estruturada de incompatibilidade par a par.** O padrão do
mercado inteiro é *ícone + nota livre + pop-up no balcão*. E não é descuido — são duas razões:

1. **Econômica.** Cuidado vira software quando é **faturável** ou quando **o tutor
   reclama**. Medicação é as duas coisas → bem resolvida. **Reatividade não é nenhuma das
   duas** → não existe em produto nenhum.
2. **Jurídica.** Afirmar "esses dois podem ficar juntos" é assinar embaixo quando dá briga.

**A saída do CãoMetria para as duas:** *registro, não recomendação*. A coleira espelha o
que a creche registrou; a ocorrência descreve o que aconteceu. O app nunca declara que um
cão é seguro.

### O que NÃO foi verificado — não afirmar como fato

- `support.gingrapp.com` devolveu **HTTP 403**. As citações de doc do Gingr vieram de
  trechos indexados. **Não foi possível** contar artigos por categoria nem confirmar o
  que o plano Play inclui de fato.
- Não há changelog público de MoeGo, Sispet, Paw Partner nem Revelation Pets — a análise
  de changelog é **amostra de um** (Gingr).
- Preço de Sispet e Milisa é sob consulta — packaging no mercado BR não foi testado.
- **Nenhum relato real de operador** (Reddit/fóruns) sobre erro de medicação ou briga em
  creche foi encontrado. É a maior lacuna da pesquisa.
- PetExec, Time To Pet, Ledog PRO, Sistema Pet, HostMyPet, Pet Attend, Milisa,
  DoggieDashboard, Paw Partner, DatCog **não foram investigados a fundo** — aparecem no
  levantamento, não na análise.

---

## 5. A primeira fatia e as premissas

**Critério de corte:** entra o que fecha o ciclo **informação → execução → comprovação**
para um cão, em um dia.

**Dentro (tudo construído e clicável):** prontuário com coleira derivada · check-in com
instrução da coleira física · painel por severidade com filtro · tarefas com comprovação ·
alerta que insiste (adiar só 2×) · dose atrasada com contador · **saída bloqueada por
pendência** · check-out com quem levou (inclusive terceiro autorizado) · edição com
recálculo da coleira · virada do dia · **registro de ocorrência**.

**Fora, de propósito:** reserva, cobrança, pagamentos, portal do tutor, perfil individual
de funcionário, relatórios/indicadores, vacinas, banho & tosa, multi-unidade.

### Premissas assumidas (se alguma cair, o escopo muda)

- **P1 — A comprovação assina com a conta da creche, não com uma pessoa.** Login único do
  estabelecimento. Responsabilização individual é Horizonte 2.
- **P2 — Um aparelho por creche, no balcão do atendimento.** Quem o opera **não administra
  o remédio — garante que alguém administrou**. *Esta é a premissa mais importante e a
  mais atacável: é exatamente onde o Gingr falha (alerta longe do risco). Foi assumida de
  propósito, e o celular de cada cuidador é o **item 1 do Horizonte 2**.*
- **P3 — O alerta é alarme local agendado no aparelho**, não push de servidor. É o que
  atende "tocar com o app fechado" sem backend.
- **P4 — Tarefas só valem para pets presentes.**
- **P5 — Aviso de dose não administrada é presencial, no check-out.** Canal do tutor é futuro.

### Métricas

| | Métrica | Por quê |
|---|---|---|
| **Principal** | % de doses administradas **no horário devido** | Mede a promessa, e o denominador vem do prontuário |
| **De atrito** | **Adiamentos por alerta disparado** | Se sobe, o alarme toca na hora errada. O protótipo já conta |

**Deliberadamente não é métrica de operação: número de acidentes.** É raro demais para
dirigir, o próprio produto muda a subnotificação (sobe quando funciona), e como placar
cobra imposto sobre a honestidade de quem registra. Estrela-guia anual, com denominador
(por 1.000 cão-dia) e ponderada por gravidade. **Corolário de desenho: o registro nunca
alimenta avaliação individual de funcionário.**

---

## 6. O protótipo — como ele realmente funciona

`prototipo/index.html`, HTML+CSS+JS puro, sem dependências. Abrir com duplo clique.

### Controles (importante — não existe "avançar o relógio" livre)

| Controle | O que faz |
|---|---|
| **Sino 🔔 no cabeçalho** | `fireAlert()` — dispara o alarme de medicação. **É o botão da demo** |
| **Clicar no relógio** | `virarDia()` — vira o dia. **Cuidado para não clicar sem querer** |
| Adiar uma dose | Única coisa que avança o relógio (+5 min) |

### Estado inicial

- Relógio em **14:00**, dia 1. Login: conta única (`Creche Patas Felizes`).
- **Bila** 🐶 verde, presente — sem apontamentos.
- **Nina** 🐩 amarela, presente — ração sem grãos 12:00 (**já atrasada às 14:00**),
  Apoquel 5mg 14:00, alergia a frango, dois tutores (guarda compartilhada).
- **Thor** 🦮 vermelha, presente — reativo. Já tem **uma ocorrência semeada** às 09:40
  (separação preventiva com a Bila), espelhada no prontuário da Bila.
- **Mel** e **Zeca** — cadastrados, sem check-in.
- `RE_ALERTA_MS = 8000` (8s no protótipo = 5 min no app real) · `MAX_ADIAMENTOS = 2`.

### Armadilhas conhecidas no código

- **`esc(s)`** é uma função só, usada tanto para atributo (`value="…"`) quanto para texto
  livre. Escapa `& < > "`. **Não criar uma segunda `esc`** — houve colisão por hoisting.
- **`fireAlert()` desiste se `state.occ` estiver preenchido.** Sem isso, o alarme
  re-disparando a cada 8s reescreve o overlay e destrói o formulário de ocorrência aberto.
- **Ocorrência grava nos dois cães** quando há outro envolvido. É de propósito: forma o
  histórico de convivência do Horizonte 2.
- **Ocorrência não altera a coleira.** Também de propósito, e há um aviso fixo no modal
  dizendo isso. É a Regra 3 aplicada.

### Roteiro de demo (6 passos, ~7 min)

1. **Painel às 14:00** — Thor no topo por severidade, comida da Nina já atrasada.
   *"O painel já está me cobrando."*
2. **Filtro vermelho** — quem isolar agora.
3. **Check-in da Mel** — coleira amarela derivada + instrução física. *"Aqui o digital
   vira físico. O cão não carrega o app; a coleira, sim."*
4. **Sino 🔔** — alarme do Apoquel. **Adiar uma vez** (vai para 14:05), deixar
   re-disparar sozinho, **adiar de novo** → "não é mais possível adiar". Confirmar.
5. **Check-out da Nina** → **bloqueio**, porque a comida das 12:00 segue pendente.
   **Parar aqui.** *"Nenhuma ferramenta que analisei impede o cão de sair com cuidado
   pendente. É a diferença entre lembrar e garantir — e é o verbo que o case usou."*
6. **Thor** → banner de reatividade + ocorrência de 09:40 → registrar uma nova com a Bila
   → abrir a **Bila** e mostrar o mesmo registro. *"Cada registro entra nos dois
   prontuários. E note: o app não disse que eles podem ficar juntos. Disse o que aconteceu."*

---

## 7. O deck

`docs/apresentacao.html` — 15 slides, scroll-snap, navegação por setas ↑↓→, toggle de tema
claro/escuro no canto.

| # | Slide | Papel |
|---|---|---|
| 1 | Capa | |
| 2 | Contexto | Os três exemplos do case |
| 3 | Processo | 8 passos, de discovery a protótipo |
| 4 | Discovery | 12 ferramentas, 3 a fundo |
| 5 | Matriz | A tabela competitiva |
| 6 | **Como li a tabela** | Material **defensivo** — onde fui generoso e por quê |
| 7 | Brainstorm | O espaço em branco |
| 8 | **Por que o vazio** | Razão econômica + jurídica. **Melhor momento intelectual** |
| 9 | Insight | Inversão pet-cêntrica |
| 10 | Triagem | A coleira e as 3 regras |
| 11 | Visão | |
| 12 | 1ª fatia | Critério de corte + os 10 itens + premissa P2 |
| 13 | Métricas | As duas métricas + o que não sei |
| 14 | Como usei IA | 6 papéis, incl. "advogada do diabo" |
| 15 | Adiante | Três horizontes |

**Decisões de layout já tomadas:** `justify-content: safe center` nos slides (conteúdo alto
encosta no topo em vez de sangrar), padding vertical 72/78px, lista de escopo compacta.
Cuidado com a regra global `p{max-width:62ch}` — ela vaza para parágrafos dentro de
containers largos e cria colunas estreitas indesejadas.

---

## 8. Próximos passos

### P0 — antes da conversa

1. **Abrir `prototipo/index.html` no navegador e clicar o roteiro inteiro dos 6 passos.**
   As últimas mudanças (registro de ocorrência) **nunca foram executadas em navegador** —
   a validação feita foi só estática (balanço de chaves, funções duplicadas, referências).
   Testar em especial: Thor → Ocorrências → registrar com a Bila → conferir se aparece
   nos dois prontuários.
2. **Abrir `docs/apresentacao.html` e conferir se algum slide estoura a altura da tela.**
   Ordem de risco: **1ª fatia** (mais denso) → **Como usei IA** (6 cards em uma linha, ~165px
   cada, pode ficar apertado; se ficar, quebrar em duas linhas de 3) → Métricas → Por que o vazio.
   Teste rápido: se precisar de `Ctrl+-` para caber, precisa de ajuste.
3. **Ensaiar**, com o cronômetro. 25 min de apresentação comprimível para 12. Sacrificar
   Discovery e Matriz se cortarem o tempo — **nunca a demo nem o slide 8**.
4. **Testar o compartilhamento de tela** com o protótipo em janela estreita (é mobile-first;
   janela larga fica feia) e o deck no tema certo.
5. **Deixar três abas abertas** durante a conversa: deck, protótipo e
   `docs/anexo-analise-competitiva.md`. O anexo é o que se abre se questionarem a matriz —
   principalmente sobre os produtos que não foram investigados a fundo (ver §9).

### P1 — se sobrar tempo

5. **Escrever a história 13 — "Registrar uma ocorrência".** O índice em
   `historias/historias-caometria-primeira-fatia.md` lista 12 e afirma que *"todos os itens
   já estão implementados"*. O registro de ocorrência foi adicionado depois e **não tem
   história nem critério de aceite**. É a última inconsistência entre os artefatos.
6. **Adicionar a Tela 7 (registro de ocorrência)** em `design/telas-primeira-fatia.md`.
   O arquivo já tem a Tela 6 (check-out & bloqueio), mas não a de ocorrência.
7. Atualizar a métrica: com ocorrência registrável, **"intervenções preventivas
   registradas"** vira métrica antecedente disponível — vale citar como o que passa a ser
   mensurável a partir desta fatia.

### Fora de escopo — não fazer

Não construir cobrança, portal do tutor, agenda comercial nem relatório gerencial. É onde
Gingr, MoeGo e Sispet colocaram os últimos dois anos de engenharia, e entrar por ali é
chegar tarde no lugar mais cheio. Se a conversa puxar para lá, a resposta é o slide 8.

---

## 9. Perguntas difíceis, com resposta

| Pergunta | Resposta |
|---|---|
| *"Por que não começar pelo cadastro/agenda?"* | A informação já existe; o que falha é chegar ao turno. Cadastro fecha ~20% da dor |
| *"Por que não assinar o Gingr por US$142?"* | Se a dor for cobrança e ocupação, é a resposta certa. Não é, se for garantir cuidado |
| *"O MoeGo já imprime etiqueta de coleira"* | Etiqueta é documento que se lê de perto; coleira é **sinalização de severidade**, legível do outro lado do salão |
| *"Se o vazio é óbvio, por que ninguém fez?"* | Não é faturável, e afirmar segurança gera responsabilidade civil. **Slide 8** |
| *"E se o app errar a cor e o cão morder alguém?"* | A cor não é laudo — espelha o que a creche registrou. **Regra 3** |
| *"Quem recebe o alerta? Está onde o risco acontece?"* | **Não, e eu sei.** Premissa P2, assumida de propósito; item 1 do Horizonte 2. **Entregar isso antes de perguntarem** |
| *"E se a equipe não registrar?"* | Principal risco. Dois toques no máximo, e o registro nunca alimenta avaliação individual |
| *"Como mede sucesso?"* | % de doses no horário e adiamentos por alerta. Acidente é estrela-guia anual, não painel semanal |
| *"Por que 'CãoMetria' se a fatia não mede nada?"* | O nome é a promessa dos horizontes; a fatia produz o dado que os indicadores vão ler |
| *"Como você sabe que o PetExec / Time To Pet / Ledog PRO tem isso?"* | **Não sei — e não defender.** Esses três estão marcados na matriz do slide 5 mas **não foram investigados a fundo**. Resposta: *"esse eu levantei, não investiguei — fui a fundo em três, e está anotado qual é qual."* A tabela de profundidade está no anexo. Ter isso escrito transforma a lacuna em rigor; defender marcação não verificada faz o contrário |

### Fechamento sugerido

> *"Com mais dois dias eu faria três coisas: o celular de cada cuidador, para o alerta
> tocar onde o risco está; o painel de indicadores, para as duas métricas saírem do
> registro manual; e sentaria um dia na creche para descobrir se os incidentes vêm de
> informação faltando ou de gente faltando — porque se for o segundo, software nenhum
> resolve."*

---

## 10. Como a IA foi usada (é avaliado — não improvisar)

Três movimentos, todos verdadeiros e demonstráveis:

1. **Pesquisa com citação obrigatória.** Subagente com acesso à web, proibido de inventar
   concorrente; cada afirmação com link e data de acesso. Ver §4.
2. **Falsificação, não confirmação.** A tese *"essas ferramentas se preocupam mais com o
   financeiro"* foi enviada para ser **derrubada**, não confirmada. Resultado: parcialmente
   verdadeira — **certa no efeito, errada na causa**. Não é desinteresse pelo pet; é que
   cuidado só vira software quando é faturável. **Essa correção virou o slide 8.**
3. **Honestidade sobre o limite do dado.** Quando `support.gingrapp.com` devolveu 403, o
   relatório voltou com *"não consegui verificar — não estimei"* em vez de um número
   plausível.

**A divisão:** eu decido visão, priorização e o que fica de fora; a IA executa pesquisa,
síntese, código, e me contradiz.
