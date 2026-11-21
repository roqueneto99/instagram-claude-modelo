# Manutenção

## Dois vencimentos para pôr na agenda

1. **O GH_PAT vence.** É o token do GitHub que deixa a renovação mensal funcionar. A validade é escolhida na criação (até um ano) e fica anotada no `instalacao.md`. Quando vencer, a Action "Renovar token do Instagram" começa a falhar e, em até 60 dias, a publicação para. Crie outro uma semana antes e atualize o secret `GH_PAT`. Basta pedir ao Claude: "renova o GH_PAT".
2. **O GitHub desliga agendamentos depois de 60 dias sem commit.** Vale para repositório público. Cada post publicado conta como commit, então quem posta com frequência nem percebe. Se ficar dois meses parado, o GitHub avisa por e-mail e desliga a renovação e o agendamento. Para religar: aba Actions, abrir cada workflow e clicar em Enable workflow. Se o token do Instagram venceu nesse intervalo, é preciso gerar outro.

## Se algo parar

Peça ao Claude: "testa a conexão". A Action "Testar conexão com o Instagram" diz o que está errado.

- Token do Instagram vencido ou inválido: gerar outro no painel da Meta e atualizar o secret `IG_ACCESS_TOKEN`.
- "Renovar token do Instagram" falhando: quase sempre é o `GH_PAT` vencido.
- Nada roda há semanas: é o item 2 acima.

## Por que o repositório é público

O Instagram baixa as imagens de um endereço público, e esse endereço é o seu repositório. Por isso só entra em `posts/` o que você já aprovou. Rascunhos ficam no seu computador. Os tokens ficam nos secrets do GitHub, que ninguém consegue ler.

## Limites

- Post único ou carrossel de até 10 imagens, e Reels de até 19 MB.
- Legenda com até 2.200 caracteres e 30 hashtags.
- Post agendado pode atrasar de minutos a horas: o relógio do GitHub não é exato.

## O que tem em cada pasta

| Caminho | Para que serve |
|---|---|
| `COMECE-AQUI.md` | A mensagem única de instalação |
| `.claude/commands/instalar.md` | O roteiro que o Claude segue |
| `CLAUDE.md` | Regras fixas e o seu design system |
| `design/` | Base visual dos posts |
| `posts/` | Um post por pasta. Só sai o que estiver `aprovado` |
| `scripts/` e `.github/workflows/` | Preparar, publicar, renovar o token e testar a conexão |
| `docs/etapa-3-acompanhamento.md` | Proposta opcional de acompanhamento de resultados (ainda não construída) |
