> Parte de **[CãoMetria — primeira fatia](historias-caometria-primeira-fatia.md)**.
> Contexto, escopo, premissas e perguntas em aberto estão no índice.

# História 7 — Ser alertado no horário da dose, mesmo com o app fechado

**Prioridade:** P0
**Depende de:** História 3

> **Como** atendente da creche
> **quero** que o celular do balcão toque no horário de cada dose e insista a cada 5
> minutos até a dose ser resolvida
> **para que** nenhuma medicação dependa de alguém lembrar de olhar a tela

### Critérios de aceite

**CA1 — o alarme toca com o app fechado**
```gherkin
Dado que a Nina está presente com Apoquel 5mg agendado para 14:00
E o app está fechado no celular do balcão
Quando o relógio chega às 14:00
Então o celular emite uma notificação com som, identificando o pet, o medicamento, a dose e o horário
```

**CA2 — a notificação leva direto à ação**
```gherkin
Dado que a notificação da dose está na tela
Quando toco nela
Então o app abre na confirmação daquela dose específica
```

**CA3 — insiste a cada 5 minutos**
```gherkin
Dado que a notificação das 14:00 não foi respondida
Quando se passam 5 minutos sem confirmação
Então o alerta é emitido novamente
E continua se repetindo a cada 5 minutos enquanto a dose não for resolvida
```

**CA4 — confirmar encerra a insistência**
```gherkin
Dado que o alerta da dose está se repetindo
Quando confirmo a dose, pela notificação ou dentro do app
Então o alerta para de repetir
E a dose fica registrada com o horário real da confirmação
```

**CA5 — adiar 5 minutos, no máximo duas vezes**
```gherkin
Dado que o alerta da dose está na tela e não posso atender agora
Quando escolho "Adiar 5 min"
Então o alerta some e reaparece 5 minutos depois
```

**CA6 — o segundo adiamento é o último**
```gherkin
Dado que já adiei essa dose duas vezes
Quando o alerta reaparece
Então a opção de adiar não está mais disponível
E o alerta continua se repetindo a cada 5 minutos até a dose ser confirmada ou registrada como não administrada
```

**CA7 — o alarme fura o silencioso**
```gherkin
Dado que o celular do balcão está no modo silencioso
E a Nina tem dose agendada para 14:00
Quando o relógio chega às 14:00
Então o alerta toca com som audível, como um despertador
```

**CA8 — o alerta não pode falhar em silêncio**
```gherkin
Dado que a permissão de notificação está negada, ou o aparelho está numa configuração
que impede o alarme de tocar
Quando abro o app
Então vejo um aviso persistente de que os alertas de medicação não vão tocar
E o aviso oferece o caminho para corrigir a configuração
```

**CA9 — cada disparo e cada adiamento ficam registrados**
```gherkin
Dado que o alerta de uma dose disparou três vezes e foi adiado duas
Quando a dose é finalmente confirmada
Então o registro da dose guarda quantas vezes o alerta disparou e quantas foi adiado
```

**CA10 — sobrevive a reinício**
```gherkin
Dado que há doses agendadas para hoje
Quando o celular é reiniciado
Então os alertas das doses ainda pendentes continuam agendados
```

**CA11 — pet ausente não alerta**
```gherkin
Dado que a Mel tem dose agendada para 09:00 e não fez check-in
Quando chega o horário
Então nenhum alerta é emitido para essa dose
```

**CA12 — duas doses no mesmo horário**
```gherkin
Dado que dois pets presentes têm dose agendada para 14:00
Quando chega o horário
Então recebo um alerta por dose, cada um identificando o seu pet
E cada dose para de insistir individualmente, quando resolvida
```

### Notas técnicas
- É o requisito mais pesado tecnicamente da fatia. Alarme local agendado (premissa
  **P3**), não push de servidor. No Android exige permissão de notificação (13+) e
  provavelmente alarme exato; a otimização de bateria do fabricante pode matar o
  agendamento — o CA7 existe justamente para expor isso no teste.
- **CA7 (furar o silencioso) tem viabilidade diferente em cada plataforma** — a decisão de
  produto é a mesma, a entrega não:
  - **Android:** viável, é o comportamento de um app despertador. Canal de notificação
    com `AudioAttributes` de `USAGE_ALARM` (o silencioso do Android silencia toque e
    notificação, não o stream de alarme); `setBypassDnd(true)` para furar o Não Perturbe,
    que exige o usuário conceder acesso à política de notificação uma vez; `full-screen
    intent` para aparecer na tela travada. Atenção às restrições de política: no Android
    14 o full-screen intent é concedido automaticamente só a apps de alarme e chamada, e
    o Google Play restringe `USE_EXACT_ALARM` a apps de despertador/agenda — pode ser
    necessário pedir `SCHEDULE_EXACT_ALARM` ao usuário.
  - **iOS:** só com o *entitlement* de **Critical Alert**, solicitado à Apple e aprovado
    caso a caso (historicamente saúde, segurança e dispositivos médicos). O nível
    `.timeSensitive` fura o Foco, mas **não** o interruptor de silencioso. Sem o
    entitlement, a garantia vira regra operacional (o celular do balcão não fica no mudo)
    somada ao aviso do CA8 — ver **pergunta em aberto #9**.
- O CA8 deixa de ser só sobre permissão de notificação: precisa cobrir também o aparelho
  configurado de um jeito que impeça o alarme de tocar. Um alerta que falha calado é pior
  que não ter alerta, porque cria confiança falsa.
- O CA9 existe para a **métrica 2** (adiamentos por alerta disparado). O protótipo já
  conta cada disparo e cada adiamento por tarefa (`disparos` / `adiamentos`), que é o
  registro de que a métrica precisa.
- O limite de dois adiamentos (CA6) não é limite de insistência: passados os dois, o
  alarme continua tocando a cada 5 minutos. A única saída é resolver a dose.
- O protótipo simula tudo isso pelo sino do cabeçalho e por um relógio clicável:
  `snoozeDose()` limita a dois adiamentos e `fecharEReagendar()` reprograma o próximo
  disparo (5 min no app real, ~8 s na demo); fechar o alerta sem resolver também reagenda.

### Fora desta história
- Alerta para tarefas de alimentação — só medicação foi pedida.
- Enviar o alerta para mais de um aparelho (premissa **P2**).
