---
description: Instala a publicação no Instagram do começo ao fim, parando só onde a pessoa é obrigatória
---

Você vai instalar este publicador de Instagram para uma pessoa que usa o Claude no básico e não é programadora. Ela colou uma mensagem única e espera que você faça quase tudo. Siga este roteiro à risca.

MODELO é o endereço do repositório modelo que veio na mensagem da pessoa. DONO e REPO são a conta dela e o nome da cópia que você vai criar.

## Como conduzir

**Você faz, ela confirma.** Não pergunte o que você consegue descobrir ou fazer sozinho. Não peça permissão para cada passo. Não explique o que é GitHub, API ou token além de uma frase quando for inevitável.

**Só existem cinco motivos para parar.** Fora deles, siga em frente:
1. As três respostas do design e o "serve" do visual (Passo 1).
2. Entrar em uma conta ou criar uma: GitHub, Facebook e Instagram.
3. Confirmação de segurança: código do GitHub, senha pedida de novo, verificação em duas etapas, captcha, telefone.
4. Autorizar o Claude a usar um site no Chrome, quando o Chrome pedir.
5. Gerar e colar um token. São dois: o do Instagram e o `GH_PAT`.

**Cada parada é uma frase só**, dizendo exatamente o que ela faz e como avisar que terminou. Exemplo: "Entre no seu Instagram na janela que abriu e me diga 'pronto'." Depois espere.

**Dois modos.**
- **Assistido (padrão):** se você tem as ferramentas do Claude no Chrome, abra as páginas, clique e preencha você mesmo no navegador dela. Ela só entra nas cinco paradas.
- **Manual:** sem o Claude no Chrome, cada tela vira uma instrução curta com o link direto, uma por vez, e você confere pelo que ela descreve. Avise uma única vez, no começo: "Sem o Claude no Chrome eu te guio pelos cliques. Dá certo do mesmo jeito, só leva mais tempo."

**Token e senha: você nunca vê.**
- Nunca peça token ou senha no chat. Se ela colar um, diga para descartar e gerar outro, e não repita nem grave o valor.
- Nunca grave token em arquivo, comando, variável ou histórico.
- No modo assistido, a partir da frase em que você pede para ela gerar o token, **não olhe o navegador**: nada de captura de tela, leitura de página ou de área de transferência, em nenhuma aba, até ela dizer "pronto". O token fica visível na tela nesse intervalo.
- Para conferir, use só a lista de nomes dos secrets (`gh secret list`), que não mostra valores.

**Nada de publicar.** A instalação não publica nenhum post. O teste final só lê o perfil.

**Tela diferente do roteiro.** Os painéis mudam. No modo assistido, leia a tela e ache o equivalente. No manual, peça um print. Não invente caminho. Se travar duas vezes no mesmo ponto, diga à pessoa o que está acontecendo.

**Progresso.** Mantenha `instalacao.md` na raiz da cópia: passos concluídos, modo usado, pendências e a validade do `GH_PAT`. Se o arquivo já existir, retome de onde parou e diga isso em uma linha.

Abra com uma mensagem de três linhas: o que vai acontecer, que ela só será chamada em poucos momentos e que o primeiro post de exemplo aparece em uns 10 minutos. Na mesma mensagem já faça a primeira pergunta do Passo 1, e rode o Passo 0 enquanto ela responde.

---

## Passo 0. Preparar (sem perguntas)

1. **Você consegue agir neste computador?** Precisa rodar comandos e gravar arquivos. Se não consegue, diga em uma frase: "Abra o Claude Code no seu computador e cole a mesma mensagem lá." e pare.
2. **Modo.** Veja se as ferramentas do Claude no Chrome estão disponíveis e anote o modo.
3. **GitHub pelo terminal.** `gh --version`. Se faltar, instale (`brew install gh` no Mac, `winget install --id GitHub.cli` no Windows). Depois `gh auth status`.
   - Não está logado: rode `gh auth login --hostname github.com --git-protocol https --web`, mostre o código que aparecer e pare: "Na página do GitHub que abriu, digite o código XXXX-XXXX, autorize e me diga 'pronto'." Se ela não tem conta, a página oferece criar.
   - Não deu para instalar o `gh`: siga sem ele. Onde o roteiro usa `gh`, faça pelo Chrome no modo assistido, ou peça à pessoa no manual.
4. **Cópia pública.** `gh repo create meu-instagram --template MODELO --public --clone`, dentro da pasta Documentos dela. Se o nome já existe e é uma instalação anterior, baixe e retome. Se é outra coisa, use `meu-instagram-2`.
   - Sem `gh`: abra `MODELO/generate` no Chrome, nome `meu-instagram`, marque Public, crie, e depois `git clone`.
5. **Confira sozinho:** o repositório é da conta dela, é público e não é o próprio modelo (`gh repo view --json visibility,isTemplate,owner`); `git push --dry-run origin HEAD:main` passa; `python3 -c "import PIL"` funciona (se faltar, `pip install pillow`); existe um Chrome para renderizar a arte.
6. Crie o `instalacao.md`.

Se o login do GitHub demorar, não segure a pessoa: faça o Passo 1 em uma pasta provisória e mova o resultado para a cópia quando ela existir.

---

## Passo 1. Design em 10 minutos

Três perguntas, uma por vez. São as únicas.

1. "Qual é o @ do Instagram onde vamos publicar? Ele precisa estar como conta profissional (Criador de conteúdo ou Empresa). Se não souber se está, me diga que eu mostro onde ver."
   - Se for conta pessoal: no aplicativo, Configurações e atividade > Tipo de conta e ferramentas > Mudar para conta profissional. Qualquer opção serve. Não precisa de Página do Facebook.
2. "Em uma frase: sobre o que é o seu perfil e para quem você fala?"
3. "Me mande o print de um post de que você gosta, seu ou de outra pessoa. Vou usar como referência de visual."
   - Link do Instagram não serve, peça o print. Se ela não tiver nenhum, siga com o visual padrão da base.

Daí em diante não pergunte mais nada. Decida você e marque como sugerido:
- **Cores e peso visual:** tire da referência (fundo, texto, destaque). A referência orienta o estilo. Não copie logo, texto, foto ou arte de outra pessoa.
- **Fontes:** um par do Google Fonts parecido com o da referência.
- **Tom de voz:** deduza do assunto e do público.
- O restante da Parte 2 do `CLAUDE.md` já vem com padrão.

Depois:
1. Preencha os campos `PREENCHER` da Parte 2 do `CLAUDE.md`.
2. Ajuste as variáveis de cor e fonte no começo de `design/base-post.html`.
3. Gere um post de exemplo com um assunto real do perfil dela, em `rascunhos/exemplo-visual/`, pelo comando de render do `CLAUDE.md`. Abra o PNG e confira antes de mostrar.
4. Mostre o PNG com uma frase: "Esse visual serve para começar? Dá para mudar qualquer coisa depois." Se ela pedir ajuste, faça no máximo duas rodadas agora e deixe o resto para depois da instalação.

O exemplo tem de aparecer em até 10 minutos depois da terceira resposta. Não faça base de carrossel agora: ela nasce no primeiro carrossel que a pessoa pedir.

Confere: `grep -cE "(: |- )PREENCHER" CLAUDE.md` devolve 0 e ela disse que serve. Faça commit e push do `CLAUDE.md` e de `design/`. Aprovar o visual não publica nada.

---

## Passo 2. Meta

Objetivo: um app da Meta ligado ao Instagram dela e o token salvo no GitHub sem passar por você.

**O que você faz no modo assistido (no manual, vira instrução, um clique por vez):**

1. Abra https://developers.facebook.com/apps.
   - Parada, se não estiver logada ou sem cadastro de desenvolvedor: "Entre no Facebook e conclua o cadastro de desenvolvedor na página que abriu (a Meta pede para confirmar telefone ou e-mail). Me diga 'pronto'."
2. "Criar app". Nome: "Publicador" mais o primeiro nome dela. A Meta recusa nomes com "Instagram", "Insta", "IG", "Gram", "Facebook", "Face" ou "FB". Caso de uso: "Gerenciar mensagens e conteúdo no Instagram". Se pedir tipo de app, "Empresa". Se perguntar por portfólio empresarial, siga sem conectar.
   - Parada, se a Meta pedir a senha de novo: "Digite sua senha do Facebook na janela e me diga 'pronto'."
3. No app: "Casos de uso" > "Personalizar" > "Configuração da API com login do Instagram". Em painéis antigos: "Adicionar produto" > Instagram > "API com login do Instagram". Tem que ser a opção com login do **Instagram**; a de login do Facebook exige Página e não serve.
4. Confira que as permissões incluem `instagram_business_basic` e `instagram_business_content_publish`. Adicione a segunda se faltar.
5. "Funções do app" > "Funções" > "Adicionar pessoas" > "Testador do Instagram" > o handle dela.
6. Aceite o convite em https://www.instagram.com/accounts/manage_access/ > "Convites de testador" > "Aceitar".
   - Parada, se o Instagram não estiver logado no Chrome: "Entre no seu Instagram nesta aba e me diga 'pronto'."
7. De volta ao app, em "Gerar tokens de acesso": "Adicionar conta".
   - Parada: "Na janela que abriu, entre no seu Instagram, clique em permitir e me diga 'pronto'."
8. Em outra aba, abra https://github.com/DONO/REPO/settings/secrets/actions/new e preencha só o campo Name com `IG_ACCESS_TOKEN`.
9. **Parada do token.** Diga exatamente: "Agora é com você: na aba da Meta, clique em 'Gerar token' e copie. Na aba do GitHub, cole no campo Secret e clique em 'Add secret'. Feche o aviso do token na Meta e me diga 'pronto'." A partir daqui não olhe o navegador até o "pronto".
10. Confere: `gh secret list` mostra `IG_ACCESS_TOKEN`. Sem `gh`, abra https://github.com/DONO/REPO/settings/secrets/actions e veja o nome na lista.

O app fica em modo de desenvolvimento. Não envie para análise nem publique o app: nesse modo ele funciona para a conta que tem função nele, que é a dela. O token vale 60 dias e o repositório renova sozinho todo mês.

---

## Passo 3. Os outros dois secrets

**3.1 IG_USER_ID (você faz sozinho).** É o número da conta, não é segredo.
- Rode o teste: `gh workflow run testar-conexao.yml`, depois `gh run watch` e `gh run view --log`. Ele falha de propósito e mostra "Falta o secret IG_USER_ID. O valor certo, sem os espaços, é: ...".
- Tire os espaços e grave: `gh secret set IG_USER_ID --body NUMERO`.
- Sem `gh`: rode o workflow pela página https://github.com/DONO/REPO/actions/workflows/testar-conexao.yml, leia o resumo da execução e preencha o formulário de secret com o número.
- Se a falha for "Token inválido", o token foi colado pela metade: repita os itens 8 a 10 do Passo 2.

**3.2 GH_PAT.** É a chave do GitHub que deixa o repositório renovar o token do Instagram todo mês.
1. Abra o formulário já preenchido:
   `https://github.com/settings/personal-access-tokens/new?name=renovar-instagram&description=Renova+o+token+do+Instagram&target_name=DONO&expires_in=365&secrets=write`
2. Confira e complete na tela: "Repository access" em "Only select repositories" com só o REPO marcado; em permissões de repositório, "Secrets" como "Read and write"; validade a maior que a tela aceitar. Se o link não preencher, preencha à mão.
3. Em outra aba, abra o formulário de secret e preencha só o Name com `GH_PAT`.
4. **Parada do token.** Diga exatamente: "Agora é com você: na aba do token, clique em 'Generate token' (o GitHub pode pedir sua senha) e copie. Na outra aba, cole no campo Secret e clique em 'Add secret'. Feche a aba do token e me diga 'pronto'." Não olhe o navegador até o "pronto".
5. Confere: `gh secret list` mostra `GH_PAT`, `IG_ACCESS_TOKEN` e `IG_USER_ID`.
6. Anote a data de validade no `instalacao.md`.

---

## Passo 4. Prova (você faz sozinho)

**4.1 Conexão.** Rode `testar-conexao.yml` de novo. Esperado: **"Conexão OK"** com o @ dela.
- "não bate com o token": refaça o 3.1.
- "não tem a permissão de publicar": volte ao item 4 do Passo 2, adicione `instagram_business_content_publish` e repita os itens 7 a 10.
- Aviso para habilitar workflows na aba Actions: habilite e rode de novo.

**4.2 Renovação.** Rode `renovar-token.yml`. Esperado: "Token renovado". Depois rode o 4.1 mais uma vez.
- "A Meta recusou a renovação" com token recém-criado não é defeito: anote no `instalacao.md` para repetir amanhã e siga.
- Mensagem sobre o `GH_PAT`: refaça o 3.2. Esse erro só apareceria daqui a um mês, por isso o teste é agora.

**Só declare a instalação concluída com "Conexão OK" no 4.1.** Sem isso, diga com clareza que não terminou e qual é o ponto pendente.

---

## Encerramento

1. Atualize o `instalacao.md` e faça commit e push. Antes, confira que nenhum arquivo contém token.
2. Diga à pessoa, em quatro linhas:
   - está instalado, e o teste deu "Conexão OK";
   - para postar: "faz um post sobre ...", e nada sai sem ela dizer "publica";
   - duas datas para a agenda: a validade do `GH_PAT` (diga a data), e que o GitHub desliga tudo depois de 60 dias sem post. Detalhes em `docs/manutencao.md`;
   - se algo parar: "testa a conexão".
3. Ofereça fazer o primeiro post de verdade agora.

A etapa 3 (acompanhar resultados) é opcional e ainda não existe. Só mencione se ela perguntar: a proposta está em `docs/etapa-3-acompanhamento.md`.
