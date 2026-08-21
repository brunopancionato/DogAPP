# CãoMetria — Visão de Produto
*Nome de trabalho provisório. App de cuidado para creches de cães.*

---

## 1. A visão

> **Nenhum cuidado é esquecido. Toda creche opera com a segurança de um bom pronto-socorro — e todo tutor confia que seu cão está bem cuidado.**

O CãoMetria transforma a rotina caótica de uma creche de cães numa operação de cuidado
previsível e segura. Cada pet tem um **prontuário**; o sistema transforma esses
prontuários na **rotina do dia**; e uma **linguagem visual de triagem** (verde /
amarelo / vermelho) mantém o risco de cada animal sempre à vista — no mundo físico
e na tela.

---

## 2. O problema

Uma creche recebe dezenas de cães por dia, com poucos cuidadores e necessidades
espalhadas ao longo do dia. Garantir cuidado individualizado nesse ambiente é difícil
e os erros são caros — de saúde, de segurança e de confiança:

- **Dieta** — alguns pets têm alimentação específica em horários determinados.
- **Medicação** — alguns pets precisam de remédio em horários determinados.
- **Reatividade** — alguns pets são reativos/agressivos e precisam ficar isolados.

Um remédio esquecido, a comida errada ou um cão reativo no grupo errado não são
"bugs de processo": são incidentes que quebram a confiança do tutor e podem
machucar um animal — ou um funcionário.

O cuidado também é com a equipe. Um sinal visual claro de que o pet é reativo faz
o cuidador ajustar o manejo *antes* de se aproximar (abordagem mais calma, contenção
adequada), prevenindo acidentes de trabalho. A mesma linguagem de triagem que protege
os cães protege quem cuida deles.

---

## 3. O insight central: um produto **pet-cêntrico**

As ferramentas do mercado nasceram como **software de gestão/faturamento**. Nelas, o
**dono é o cliente** e o **pet é um registro subordinado** à conta de cobrança:

```
Mercado hoje:                     CãoMetria:

DONO (cliente / pagador)          PET (o "matriculado" — prontuário)
  └── Pet 1 (sub-registro)          └── Tutor A (contato)
  └── Pet 2                         └── Tutor B (contato)
```

Nós **invertemos a entidade central.** O pet é o "paciente matriculado" — dono de
seu próprio prontuário (dieta, medicação, reatividade, histórico). Os tutores são
**contatos** daquele animal (um pet pode ter vários).

Essa decisão de arquitetura não é filosófica — é o que destrava tudo:

1. **Um pet, vários tutores** funciona de forma natural — incluindo **guarda
   compartilhada** (o mesmo cão frequentando a creche a partir de dois lares após uma
   separação), cenário que no modelo centrado-no-dono vira conta duplicada.
2. **O cuidado é cidadão de primeira classe**, não um módulo pendurado numa fatura.
3. **A operação do dia flui do pet**, respondendo à pergunta que o cuidador faz de
   verdade: *"quais pets estão aqui hoje e o que cada um precisa agora?"*

---

## 4. Os atores

| Ator | Papel | Prioridade |
|------|-------|:----------:|
| **Pet** | Sujeito do sistema — o prontuário em torno do qual tudo gira | Centro do **modelo** |
| **Pessoa do atendimento** | Opera o app na 1ª fatia: recebe o alerta, registra o que foi feito, avisa quem está no chão. **Não administra o remédio — garante que alguém administrou** | Centro da **experiência** |
| **Cuidador / tratador** | Executa o cuidado no chão. Recebe a informação pela coleira física e pelo aviso da recepção. **Ganha app próprio no Horizonte 2** | Beneficiário na 1ª fatia |
| **Gestor da creche** | Configura pets, vê a operação, garante o padrão | Secundário |
| **Tutor** | Contato do pet; no futuro, recebe visibilidade | Fora da 1ª fatia |

> **Por que assim, e não o contrário.** A creche opera hoje com **um aparelho, no balcão**
> (premissa P2 das histórias). Colocar o app no bolso de cada cuidador é melhor e está
> no Horizonte 2 — mas seria projetar para uma realidade que ainda não existe. A
> consequência precisa ficar dita: **este é exatamente o ponto onde o Gingr falha** — o
> alerta dele dispara na recepção, longe de onde o risco acontece. Assumimos a mesma
> limitação de propósito na 1ª fatia, e é o primeiro item que muda depois.

---

## 5. A metáfora organizadora: triagem de pronto-socorro

No check-in, cada pet recebe uma **coleira colorida** que resume seu maior risco —
visível do outro lado do salão, sem precisar de tela:

| Cor | Significado | Natureza |
|:---:|-------------|----------|
| 🟢 **Verde** | Sem restrições ou apontamentos | Tranquilo |
| 🟡 **Amarela** | Apontamento alimentar, de medicação ou alergia | **Tarefa** — o que o cuidador *faz* |
| 🔴 **Vermelha** | Reativo / comportamento agressivo | **Estado** — *onde* o pet fica (isolamento) e *como* a equipe o maneja |

Três regras de ouro:

- **A cor é derivada do prontuário**, não atribuída na mão — o app calcula e instrui
  o cuidador ("Thor chegou → coleira AMARELA"). Menos erro humano.
- **A cor mostra a maior severidade; o prontuário carrega tudo.** Um pet reativo que
  também toma remédio usa coleira **vermelha** (segurança manda no físico), mas o card
  dele continua exibindo o apontamento amarelo.
- **A cor não é um laudo de segurança** — ela espelha o que a creche registrou. Quem
  avalia comportamento é a creche; o app só impede que o que ela já sabe fique preso na
  ficha. É a diferença entre **sinalizar** e **atestar**, e ela é deliberada: atestar
  segurança é assumir responsabilidade civil por uma briga — a razão pela qual o
  mercado inteiro parou no ícone consultivo (ver seção 6).

Isso separa limpo as duas naturezas: **amarelo = tarefa** (comida/remédio),
**vermelho = espaço** (isolamento).

A coleira vermelha protege em **três direções** ao mesmo tempo — um enquadramento que
nenhum concorrente tem (pra eles, reatividade é só "uma nota de comportamento"):

- 🐕 **o próprio pet reativo** — manejo adequado, menos estresse;
- 🐕‍🦺 **os outros cães** — evita brigas no grupo errado;
- 🧑‍🔧 **a equipe** — o sinal visual antecede a aproximação e previne acidentes de trabalho.

---

## 6. Posicionamento: onde a gente ganha

A análise competitiva levantou **12 ferramentas** (Brasil + global) e foi a fundo em
**três** — Gingr, MoeGo e Sispet — lendo documentação, tabela de planos e changelog, e
não só a página de marketing. Ela mostra dois blocos de funcionalidade:

- **Bloco "commodity"** (reserva, cobrança, portal do tutor, check-in): **todos têm.**
  É paridade — não brigamos aqui.
- **Bloco "cuidado & segurança"** (triagem visual, painel do cuidador, isolamento por
  reatividade): é um **vazio no mercado inteiro.**

**Sendo justo com os concorrentes**, porque um vazio só vale alguma coisa se o resto
estiver forte: o **MoeGo** é bom em cuidado — alimentação e medicação com horário de
relógio, dose, atribuição a um funcionário específico e desfecho padronizado — e chega a
imprimir o checklist do dia por horário e **etiqueta de coleira**. Nossa diferença não é
registrar: é **sinalizar severidade**, legível do outro lado do salão. Um é documento; o
outro é sinalização. Já o **Gingr** agenda medicação por *janela* ("AM", "Lunch") e não
por relógio, e seu alerta de comportamento é um pop-up que dispara **no balcão**, ao
mexer na reserva.

O dado que resume o setor: o plano do Gingr para **creche** (Play, US$142/mês) não lista
alimentação nem medicação entre seus diferenciais; o de **hospedagem** (Stay, US$154)
lista. Cuidado é argumento de venda de hotel — para creche, vende-se reserva e ocupação.

### Por que esse vazio existe — e não é descuido

A pergunta que precisa ser respondida antes de apostar no espaço em branco: se é tão
óbvio, por que doze produtos não o preencheram? Há duas razões, e nenhuma é distração.

1. **Econômica.** Uma capacidade de cuidado vira software quando é **faturável** ou
   quando **o tutor reclama**. Medicação é as duas coisas — o Gingr documenta cobrança
   automática por administração de medicamento, e o MoeGo tem "feeding and medication
   fee" em beta. **Reatividade não é faturável em lugar nenhum**, e o tutor não reclama
   dela até haver briga — quando já não é reclamação. Zero razão comercial para
   construir.
2. **Jurídica.** Um software que afirma "esses dois cães podem ficar juntos" assina
   embaixo quando dá briga. Daí o ícone consultivo em todo mundo: informa sem afirmar. O
   Gingr chegou mais perto e parou onde é seguro — bloquear *agendamento* pelo resultado
   da avaliação (set/2025). Gating na porta, não manejo no pátio.

**Nossa saída para as duas:** a coleira não declara que o cão é seguro, ela espelha o que
a creche registrou (regra 3 da seção 5) — e o modelo de valor não é cobrar por dose, é
reduzir risco e produzir prova, inclusive de **acidente de trabalho por mordedura**, que
já é obrigatório registrar e já custa caro à creche.

**Validação de fora do setor:** o **brightwheel**, software de creche **infantil**, faz o
que nenhum produto pet faz — registra dose e horário e alerta quando a sala sai do
**ratio adulto/criança, em tempo real**. E em Massachusetts a **"Ollie's Law"**, vigente
desde dez/2024, passou a exigir de creches caninas ratio, tamanho de grupo e reporte
obrigatório de lesão. Um estado inteiro precisou legislar porque o mercado não resolveu.

> **O espaço em branco não é uma funcionalidade que falta — é um ângulo que ninguém
> adotou:** organizar a operação em torno da *segurança do dia*, com linguagem de
> triagem. Os concorrentes são *software de gestão com um módulo de cuidado*. O CãoMetria é
> *software de cuidado e segurança* — a gestão vem depois.

---

## 7. A primeira fatia (o que priorizamos primeiro)

> **O "Painel de Triagem do dia"** — os pets presentes hoje, cada um num card com sua
> cor. No check-in, o app deriva a cor e instrui a coleira. Vermelhos aparecem
> destacados (isolar). Amarelos mostram as tarefas de cuidado do dia (comida/remédio)
> para marcar como feito. Verdes existem tranquilos.

**O critério de corte:** entra o que fecha o ciclo **informação → execução →
comprovação** para um cão, em um dia. Fica de fora tudo o que o mercado já faz bem, e
tudo o que só faz sentido depois de existir dado registrado.

**Dentro da 1ª fatia** — tudo abaixo está construído e clicável no protótipo:

- **Prontuário do pet** — dados básicos, dieta, medicação com horários, alergia,
  reatividade e **vários tutores-contato**. É a porta de entrada de todo o resto.
- **Check-in do dia** → derivação automática da cor e **instrução da coleira física**.
- **Painel do dia** com os presentes ordenados por severidade, e filtro por cor.
- **Tarefas agendadas** (comida + remédio) com marcar-como-feito e comprovação de
  quem e quando.
- **Alerta de medicação** — chegando o horário, o aparelho da creche **dispara um
  alarme** e **insiste até a dose ser resolvida**; adiar só é permitido duas vezes. É a
  diferença entre uma lista passiva ("se alguém olhar") e um sistema que cobra.
- **Dose atrasada** visível e escalada no painel, com contador de disparos e adiamentos.
- **Saída bloqueada** enquanto houver cuidado pendente — é o mecanismo que entrega o
  verbo do case: *garantir*.
- **Check-out** com registro de quem levou o pet, inclusive retirada por terceiro
  autorizado por um tutor cadastrado.
- **Edição do prontuário** com recálculo da cor e aviso para trocar a coleira física.
- **Virada do dia** preservando quem ficou em aberto.
- **Flag de reatividade** sempre visível no card e no detalhe do pet.

**Fora da 1ª fatia (deliberadamente):**
- Reserva/agenda, cobrança e pagamentos
- Portal / app do tutor
- Perfil de funcionário individual — a comprovação assina com a conta da creche
  (premissa P1); responsabilização individual é Horizonte 2
- Registro de incidentes e ocorrências
- Relatórios gerenciais e indicadores, vacinas, banho & tosa, multi-unidade

## 7.1 Como sei que deu certo

A promessa é "nada é esquecido" — então a métrica não pode ser adoção, engajamento nem
tela aberta.

| | Métrica | Por que essa |
|---|---|---|
| **Principal** | **% de doses administradas no horário devido** — confirmações dentro da tolerância, sobre o total agendado para pets presentes | Mede exatamente o que o produto promete, e o **denominador é conhecido** porque vem do prontuário |
| **De atrito** | **Adiamentos por alerta disparado** | Se subir, o alarme está tocando na hora errada ou virou incômodo em vez de tarefa. O protótipo já conta disparos e adiamentos |

**O que deliberadamente não viramos métrica de operação: número de acidentes.** É o
desfecho que justifica o produto existir, mas é raro demais para dirigir decisão, o
próprio produto muda a subnotificação (o número **sobe** quando a ferramenta funciona), e
usá-lo como placar cobra imposto sobre a honestidade de quem registra. Fica como
estrela-guia anual — com denominador (por 1.000 cão-dia) e ponderado por gravidade —,
nunca como painel semanal. **Corolário de desenho:** o registro nunca alimenta avaliação
individual de funcionário.

> O painel de indicadores está fora desta fatia. Nos primeiros 30 dias a leitura é por
> extração manual dos registros que as histórias 6, 7 e 10 já produzem.

---

## 8. Por que essa fatia

- **Entrega o coração do valor** ("nada é esquecido") no menor recorte possível.
- **É totalmente demonstrável** num protótipo — cabe numa tela.
- **Ataca a fraqueza do mercado**, não a força dele.
- **Comida + remédio compartilham o mesmo mecanismo** (tarefa agendada com
  comprovação): resolver um resolve os dois.
- **O alerta ativo de medicação** eleva a ferramenta de uma *lista passiva* ("se alguém
  olhar") para um *sistema que cobra* ("o aparelho avisa e insiste até confirmar").
- **O bloqueio da saída** é o que fecha o ciclo: sem ele o app lembra; com ele, garante.
  Nenhuma das ferramentas analisadas impede o cão de sair com cuidado pendente.
- A **reatividade** — o ponto mais fraco de todos os concorrentes — é onde a coleira
  colorida brilha.

---

## 9. Visão de longo prazo — três horizontes

O nome entrega a promessa: **CãoMetria** = medição. Começamos medindo o cuidado do
dia; evoluímos para medir a operação inteira; e terminamos organizando tudo que o cão
precisa.

### Horizonte 1 — A primeira fatia (construída)
Prontuário do pet · check-in/coleira · painel do dia · tarefas comida+remédio ·
alerta que insiste · dose atrasada · saída bloqueada por pendência · check-out com
quem levou · virada do dia · reatividade sempre visível.

### Horizonte 2 — Operação madura
- **O app no bolso de cada cuidador** — é o **primeiro item**, e não é conforto: hoje o
  alerta toca no balcão, longe de onde o risco está. Junto vem o **perfil do funcionário**
  — comprovação real (quem administrou cada dose), papéis/permissões, escala de turno.
  Alicerce da responsabilização e fecha a "3ª direção de segurança" (proteger a equipe).
- **Composição do grupo** — quem está em qual espaço, agora, com qual cuidador, e o
  ratio do ambiente. É o análogo do alerta de sala do brightwheel, e a única forma
  honesta de tratar reatividade: **registrar o que aconteceu e com quem o cão ficou**,
  em vez de afirmar que uma combinação é segura.
- **Versão web** — amplia o canal de uso: a creche opera também na tela grande
  (gestão, cadastros) e os tutores acompanham de qualquer lugar, não só pelo celular.
- **Tutor com visibilidade** — report card, "Nina tomou o remédio 14:03", receita
  veterinária.
- **Incidentes & ocorrências** — registrar brigas/mordidas, relatório de segurança.
- **Indicadores (a "metria" do nome)** — aderência à dieta/medicação, tarefas no
  horário, incidentes por período → dashboards que nenhum concorrente tem.

### Horizonte 3 — A agenda do pet: a creche como plataforma de serviços
A **agenda do pet** unifica tudo que é agendado em torno do animal — não só as tarefas
de cuidado, mas os serviços que a creche pode oferecer:
- **Banho e tosa** — agendar, registrar, notificar o tutor.
- **Adestramento** — sessões e evolução comportamental (fecha o ciclo com a
  reatividade: o cão vermelho melhora ao longo do tempo, e a CãoMetria mostra).
- **Rede de unidades** — o prontuário (e a agenda) que viaja com o pet entre creches.
