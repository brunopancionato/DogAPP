> Parte de **[CãoMetria — primeira fatia](historias-caometria-primeira-fatia.md)**.
> Contexto, escopo, premissas e perguntas em aberto estão no índice.

# História 1 — Entrar no app com a conta da creche

**Prioridade:** P0

> **Como** atendente da creche
> **quero** acessar o app com a conta da creche
> **para que** o prontuário dos pets e os telefones dos tutores não fiquem abertos para
> qualquer pessoa que pegue o celular do balcão

### Critérios de aceite

**CA1 — acesso válido**
```gherkin
Dado que estou na tela de acesso
Quando informo o usuário e a senha corretos da creche
Então entro no Painel do dia
E o nome da creche fica visível no app como identificação de quem registra as ações
```

**CA2 — credenciais inválidas**
```gherkin
Dado que estou na tela de acesso
Quando informo uma senha incorreta
Então permaneço na tela com a mensagem "usuário ou senha inválidos"
E a mensagem não revela qual dos dois campos está errado
```

**CA3 — sessão permanece ativa**
```gherkin
Dado que já entrei com a conta da creche
Quando fecho e reabro o app durante o expediente
Então entro direto no Painel do dia, sem novo acesso
```

**CA4 — falha de comunicação**
```gherkin
Dado que o celular está sem internet
Quando tento entrar
Então recebo a mensagem de que não foi possível verificar o acesso
E tenho a opção de tentar novamente
```

### Notas técnicas
- Se a validação do acesso for local no aparelho, o CA4 deixa de existir — decisão do
  tech lead.
- O identificador da conta é o que carimba toda comprovação (histórias 6, 8 e 9).

### Fora desta história
- Conta individual por funcionário e permissões por papel (Horizonte 2).
- Recuperação de senha — ver pergunta em aberto #3.
