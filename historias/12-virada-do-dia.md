> Parte de **[CãoMetria — primeira fatia](historias-caometria-primeira-fatia.md)**.
> Contexto, escopo, premissas e perguntas em aberto estão no índice.

# História 12 — Virar o dia sem perder quem ficou em aberto

**Prioridade:** P1
**Depende de:** História 8

> **Como** atendente da creche
> **quero** que o painel comece limpo a cada dia, mas mantenha visível o pet cuja saída
> ninguém registrou
> **para que** a diferença entre "o cão ficou aqui" e "alguém esqueceu de dar baixa"
> apareça, em vez de sumir na virada

### Critérios de aceite

**CA1 — o dia começa limpo**
```gherkin
Dado que ontem havia pets presentes, todos com check-out registrado
Quando abro o app no dia seguinte
Então o Painel do dia está vazio, aguardando os check-ins de hoje
```

**CA2 — pendência de saída fica à vista**
```gherkin
Dado que um pet fez check-in ontem e nunca teve check-out
Quando abro o app no dia seguinte
Então ele aparece sinalizado como "check-out não registrado", com a data do check-in
E a sinalização se distingue visualmente dos pets que chegaram hoje
```

**CA3 — resolver a pendência**
```gherkin
Dado que estou diante de um pet com check-out não registrado de ontem
Quando resolvo a pendência
Então registro qual foi o caso: a saída aconteceu e não foi registrada, ou o pet permaneceu na creche
E o painel reflete a escolha
```
> O segundo caso encosta em pernoite, que está fora do escopo desta fatia — ver pergunta
> em aberto #4.

**CA4 — as tarefas de ontem não migram**
```gherkin
Dado que um pet tinha tarefas pendentes ontem
Quando o dia vira
Então essas tarefas não reaparecem como pendentes hoje
E ficam registradas no histórico do pet como não realizadas naquele dia
```

**CA5 — o alerta de ontem não persegue**
```gherkin
Dado que uma dose de ontem nunca foi confirmada
Quando o dia vira
Então o alerta daquela dose para de se repetir
E a falha permanece registrada no histórico
```

### Notas técnicas
- Resolvido no protótipo: o check-out zera `present` (`confirmarCheckout()`) e
  `virarDia()` (clique no relógio do cabeçalho) encerra o dia — reseta as tarefas, para
  os alertas de ontem e registra no histórico o que ficou pendente e quem virou o dia sem
  check-out.
- O CA5 é a válvula de escape da História 7: sem ele, uma dose esquecida faz o celular do
  balcão apitar a cada 5 minutos indefinidamente.
