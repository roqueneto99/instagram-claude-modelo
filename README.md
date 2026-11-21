# Instagram pelo Claude

Você pede um post ao Claude, aprova a arte e a legenda, diz "publica" e ele sai no seu Instagram. Sem aplicativo de terceiros e sem custo: usa a API oficial da Meta e o GitHub.

## O que você precisa ter

- Conta no GitHub.
- Instagram em modo profissional (Criador de conteúdo ou Empresa). Não precisa de Página do Facebook.
- Conta no Facebook, para entrar no painel de desenvolvedor da Meta.
- Claude Code no seu computador.
- Cerca de uma hora e meia, de uma vez ou em partes. A instalação lembra onde você parou.

## Como instalar

1. Nesta página, clique em **Use this template** e depois em **Create a new repository**. Marque **Public**.
2. Abra o Claude Code e peça: "clone o meu repositório https://github.com/SEU_USUARIO/NOME_DO_REPOSITORIO e abra a pasta", com o endereço do repositório que você acabou de criar.
3. Digite `/instalar` e responda uma pergunta por vez.

O Claude confere cada etapa e avisa quais cliques só você pode dar. A instalação termina quando o teste mostra "Conexão OK".

## Como usar depois

- "Faz um post sobre tal assunto": o Claude monta e mostra.
- Você pede ajustes até gostar.
- "Publica": só aí o post vai ao ar, e o Claude devolve o link.

Nada é publicado sem o seu "publica" para aquele post.

## Por que o repositório é público

O Instagram baixa as imagens de um endereço público, e esse endereço é o seu repositório. Por isso só entra em `posts/` o que você já aprovou. Rascunhos ficam no seu computador. Seus tokens ficam nos secrets do GitHub, que ninguém consegue ler.

## Dois vencimentos para pôr na agenda

1. **O GH_PAT vence.** É o token do GitHub que deixa a renovação mensal funcionar. Você escolhe a validade ao criar (até um ano). Quando vencer, a Action "Renovar token do Instagram" começa a falhar e, em até 60 dias, a publicação para. Marque na agenda para criar outro uma semana antes e trocar o secret `GH_PAT`.
2. **O GitHub desliga agendamentos depois de 60 dias sem commit.** Vale para repositório público. Cada post publicado conta como commit, então quem posta com frequência nem percebe. Se ficar dois meses parado, o GitHub avisa por e-mail e desliga a renovação e o agendamento. Para religar: aba Actions, abra cada workflow e clique em Enable workflow. Se o token do Instagram venceu nesse intervalo, gere outro.

Em qualquer dúvida, rode a Action "Testar conexão com o Instagram": ela diz o que está errado.

## O que tem aqui

| Caminho | Para que serve |
|---|---|
| `.claude/commands/instalar.md` | O passo a passo do `/instalar` |
| `CLAUDE.md` | Regras fixas e o seu design system |
| `posts/` | Um post por pasta. Só sai o que estiver `aprovado` |
| `scripts/` | Preparar e publicar os posts |
| `.github/workflows/` | Publicar, renovar o token e testar a conexão |
| `docs/etapa-3-acompanhamento.md` | Proposta opcional de acompanhamento de resultados (ainda não construída) |

## Limites

- Post único ou carrossel de até 10 imagens, e Reels de até 19 MB.
- Legenda com até 2.200 caracteres e 30 hashtags.
- Post agendado pode atrasar: o relógio do GitHub não é exato.
