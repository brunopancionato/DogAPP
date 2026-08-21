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
| **Cuidador / tratador** | Usuário do dia a dia — executa e comprova o cuidado no chão | Centro da **experiência** |
| **Gestor da creche** | Configura pets, vê a operação, garante o padrão | Secundário |
| **Tutor** | Contato do pet; no futuro, recebe visibilidade | Fora da 1ª fatia |

---

## 5. A metáfora organizadora: triagem de pronto-socorro

No check-in, cada pet recebe uma **coleira colorida** que resume seu maior risco —
visível do outro lado do salão, sem precisar de tela:

| Cor | Significado | Natureza |
|:---:|-------------|----------|
| 🟢 **Verde** | Sem restrições ou apontamentos | Tranquilo |
| 🟡 **Amarela** | Apontamento alimentar, de medicação ou alergia | **Tarefa** — o que o cuidador *faz* |
| 🔴 **Vermelha** | Reativo / comportamento agressivo | **Estado** — *onde* o pet fica (isolamento) e *como* a equipe o maneja |

Duas regras de ouro:

- **A cor é derivada do prontuário**, não atribuída na mão — o app calcula e instrui
  o cuidador ("Thor chegou → coleira AMARELA"). Menos erro humano.
- **A cor mostra a maior severidade; o prontuário carrega tudo.** Um pet reativo que
  também toma remédio usa coleira **vermelha** (segurança manda no físico), mas o card
  dele continua exibindo o apontamento amarelo.

Isso separa limpo as duas naturezas: **amarelo = tarefa** (comida/remédio),
**vermelho = espaço** (isolamento).

A coleira vermelha protege em **três direções** ao mesmo tempo — um enquadramento que
nenhum concorrente tem (pra eles, reatividade é só "uma nota de comportamento"):

- 🐕 **o próprio pet reativo** — manejo adequado, menos estresse;
- 🐕‍🦺 **os outros cães** — evita brigas no grupo errado;
- 🧑‍🔧 **a equipe** — o sinal visual antecede a aproximação e previne acidentes de trabalho.

---

## 6. Posicionamento: onde a gente ganha

A análise competitiva (8 ferramentas, Brasil + global) mostra dois blocos de
funcionalidade:

- **Bloco "commodity"** (reserva, cobrança, portal do tutor, check-in): **todos têm.**
  É paridade — não brigamos aqui.
- **Bloco "cuidado & segurança"** (triagem visual, painel do cuidador, isolamento por
  reatividade): é um **vazio no mercado inteiro.** O mais perto são ícones de
  "advisory" que aparecem no hover do mouse — informação que você precisa *ir buscar*.

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

**Dentro da 1ª fatia:**
- **Cadastro do pet** — criar o prontuário: dados básicos, dieta, medicação (com
  horários), reatividade, tutores-contato. É a porta de entrada de todo o resto.
- **Check-in do dia** → derivação automática da cor da coleira.
- **Painel do dia** com os pets presentes, organizados por cor.
- **Tarefas agendadas** (comida + remédio) com marcar-como-feito + comprovação
  (quem/quando).
- **Alertas de medicação no celular do cuidador** *(requisito do case)* — chegando o
  horário determinado, o app instalado no celular do funcionário **dispara uma
  notificação/alarme** para que o pet seja medicado. O alerta persiste até a dose ser
  confirmada (não deixa "morrer" por distração).
- **Flag de reatividade** sempre visível no card do pet.

**Fora da 1ª fatia (deliberadamente):**
- Reserva/agenda, cobrança e pagamentos
- Portal / app do tutor
- Relatórios gerenciais, vacinas, banho & tosa, multi-unidade

---

## 8. Por que essa fatia

- **Entrega o coração do valor** ("nada é esquecido") no menor recorte possível.
- **É totalmente demonstrável** num protótipo — cabe numa tela.
- **Ataca a fraqueza do mercado**, não a força dele.
- **Comida + remédio compartilham o mesmo mecanismo** (tarefa agendada com
  comprovação): resolver um resolve os dois.
- **O alerta ativo de medicação** atende um requisito explícito do case e eleva a
  ferramenta de uma *lista passiva* ("se alguém olhar") para um *sistema que cobra*
  ("o celular avisa e insiste até confirmar") — a diferença entre lembrar e garantir.
- A **reatividade** — o ponto mais fraco de todos os concorrentes — é onde a coleira
  colorida brilha.

---

## 9. Visão de longo prazo — três horizontes

O nome entrega a promessa: **CãoMetria** = medição. Começamos medindo o cuidado do
dia; evoluímos para medir a operação inteira; e terminamos organizando tudo que o cão
precisa.

### Horizonte 1 — A primeira fatia (já mapeada)
Prontuário do pet · check-in/coleira · painel do dia · tarefas comida+remédio ·
alerta de medicação · reatividade sempre visível.

### Horizonte 2 — Operação madura
- **Perfil do cuidador (funcionário)** — comprovação real (quem administrou cada
  dose), papéis/permissões, escala de turno. É o alicerce da responsabilidade e fecha
  a "3ª direção de segurança" (proteger a equipe).
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
