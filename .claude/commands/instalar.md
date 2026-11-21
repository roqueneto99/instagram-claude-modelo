---
description: Instala a publicação no Instagram, do zero, uma pergunta por vez
---

Você vai guiar a instalação deste repositório para uma pessoa que usa o Claude no básico. Ela não é programadora. Siga este roteiro à risca.

## Como conduzir

- **Uma pergunta por vez.** Faça a pergunta, pare e espere a resposta. Nunca mande dois pedidos na mesma mensagem.
- **Confira antes de seguir.** Cada etapa tem um "Confere". Só avance quando o confere passar. Se você não tem como conferir sozinho, peça para a pessoa dizer o que está vendo na tela.
- **Diga quem faz.** Antes de cada ação, diga "isso eu faço" ou "esse clique é só seu". Você não tem acesso ao Instagram, ao painel da Meta nem às senhas dela, e não deve pedir nenhuma senha.
- **Token nunca passa pelo chat.** A pessoa copia o token do painel da Meta e cola direto no formulário do GitHub. Se ela colar um token no chat, diga para descartar aquele e gerar outro, e não grave o valor em lugar nenhum.
- **Linguagem simples.** Sem sigla sem explicação. Mensagens curtas. Um link por vez, sempre o link direto.
- **Tela diferente do roteiro.** Os painéis da Meta e do GitHub mudam de nome e de lugar. Se a pessoa não achar um botão, peça um print ou a descrição do que ela vê e oriente por ali. Não invente caminho.
- **Guarde o progresso.** No início, crie ou leia `instalacao.md` na raiz, com a lista dos passos abaixo e o que já foi concluído. Atualize a cada etapa. Se o arquivo já existir, retome de onde parou e diga isso à pessoa.
- **Nada de publicar.** A instalação não publica nenhum post. O teste final só lê o perfil.

Comece com uma mensagem curta: o que vai acontecer (5 partes), quanto tempo leva (cerca de uma hora e meia, podendo parar e voltar) e a primeira pergunta do Passo 0.

Descubra sozinho, sem perguntar: o dono e o nome do repositório (`git remote get-url origin`) e se o comando `gh` existe e está logado (`gh auth status`). Use DONO e REPO de verdade em todos os links abaixo.

---

## Passo 0. Checagem

Quatro perguntas, uma por vez. O que faltar, ensine a criar antes de continuar.

**0.1 GitHub e repositório próprio**
- Pergunta: "Você criou este repositório pelo botão Use this template, na sua conta do GitHub, e marcou Public?"
- Confere (isso você faz): o `origin` aponta para a conta da pessoa, o repositório é público (`gh repo view --json visibility,isTemplate`, ou `curl -s https://api.github.com/repos/DONO/REPO` respondendo `"private": false`) e não é o próprio modelo (`is_template` falso).
- Se não tem conta: github.com/signup, depois voltar à página do modelo e clicar em Use this template > Create a new repository > Public.
- Se o repositório está privado: Settings > General > Danger Zone > Change visibility > Public. Explique o motivo: o Instagram baixa as imagens de um endereço público.

**0.2 Instagram profissional**
- Pergunta: "Seu Instagram está como conta profissional (Criador de conteúdo ou Empresa)?"
- Só a pessoa consegue ver. No aplicativo: perfil > menu > Configurações e atividade > Tipo de conta e ferramentas.
- Se for conta pessoal: nessa mesma tela, "Mudar para conta profissional". Qualquer uma das duas opções serve. Não precisa de Página do Facebook.
- Confere: a pessoa confirma que aparece "Painel profissional" no perfil. Anote o handle (o @) para o Passo 1.

**0.3 Conta de desenvolvedor na Meta**
- Pergunta: "Você já entrou alguma vez em developers.facebook.com e criou a conta de desenvolvedor?"
- Se não: precisa de uma conta do Facebook. Entrar em https://developers.facebook.com, clicar em "Começar" e confirmar o cadastro (a Meta pede para verificar telefone ou e-mail). Esses cliques são só dela.
- Confere: a pessoa abre https://developers.facebook.com/apps e vê a página "Apps" com o botão "Criar app".

**0.4 Claude com acesso ao GitHub**
- Isso você confere sozinho: `git push --dry-run origin HEAD:main` tem que passar.
- Se falhar: ajude a pessoa a entrar no GitHub pelo terminal (`gh auth login`, escolhendo GitHub.com, HTTPS e login pelo navegador) ou pelo aplicativo que ela usa, e teste de novo.
- Confira também as ferramentas locais: `python3 --version` e `python3 -c "import PIL"` (se faltar, `pip install pillow`).
- Se você estiver rodando em uma sessão na nuvem que só consegue enviar para outro ramo (branch) e não para a `main`, avise: a publicação só dispara na `main`. O caminho mais simples é usar o Claude Code no computador da pessoa.

Ao fim, mostre os quatro itens com "ok" e siga.

---

## Passo 1. Design system

Objetivo: preencher a Parte 2 do `CLAUDE.md` e ter um post de exemplo com o visual aprovado.

Entreviste, uma pergunta por vez. Quando a pessoa não souber responder, ofereça de duas a três opções prontas para ela escolher.

1. Handle do perfil (já anotado no 0.2, só confirme).
2. Sobre o que é o perfil e para quem ela fala.
3. Tom de voz. Ofereça três tons com uma frase de exemplo de cada, escritas para o assunto dela.
4. Cores. Se ela tem marca, peça os códigos ou um print de um post de que gosta e tire as cores de lá. Se não tem, proponha três paletas (fundo, texto, destaque).
5. Fontes. Proponha três pares do Google Fonts (título e texto) que combinem com o tom.
6. Assinatura: o que aparece em toda arte (handle, site, logo). Se tiver logo, peça o arquivo e salve em `design/`.
7. Formatos: como ela imagina o post único e o carrossel (quantas telas, como é a capa, como é a última tela).
8. Legenda: tamanho de costume, hashtags fixas, chamada final.
9. O que nunca escrever: palavras, promessas, assuntos, pontuação.

Depois:
- Preencha a Parte 2 do `CLAUDE.md`. Não pode sobrar nenhum `PREENCHER` (onde não se aplica, escreva "não tem").
- Gere um post de exemplo de 1080 x 1350 em `rascunhos/exemplo-visual/`, com um assunto real do perfil dela. Método sugerido: um arquivo HTML com as cores e fontes, renderizado em PNG por um navegador sem janela (Chrome, Chromium ou Playwright). Se não houver navegador disponível, desenhe com Pillow. Abra o PNG e confira você mesmo antes de mostrar: texto cortado, fonte errada e margem torta são os erros comuns.
- Mostre o PNG e pergunte: "Esse é o visual? O que muda?" Ajuste até ela aprovar.
- Quando aprovar, salve o arquivo que gerou a arte como base em `design/` (por exemplo `design/base-post.html`) e anote no `CLAUDE.md` o método e o comando de render que funcionaram. Faça também a base do carrossel (capa, tela do meio e última tela) e mostre.

Deixe claro para a pessoa: aprovar o visual não publica nada.

Confere: `grep -cE "(: |- )PREENCHER" CLAUDE.md` devolve 0, existe pelo menos um arquivo base em `design/` e a pessoa disse que aprova o visual. Faça commit do `CLAUDE.md` e da pasta `design/` (o exemplo em `rascunhos/` não vai para o GitHub).

---

## Passo 2. Meta

Tudo neste passo são cliques da pessoa, no navegador dela. Você orienta e confere pelo que ela descreve. Avise isso no começo e diga que leva de 20 a 30 minutos.

**2.1 Criar o app**
- https://developers.facebook.com/apps > "Criar app".
- Nome: qualquer um, por exemplo "Publicador" mais o primeiro nome dela. Aviso importante: a Meta recusa nomes com "Instagram", "Insta", "IG", "Gram", "Facebook", "Face" ou "FB".
- Caso de uso: "Gerenciar mensagens e conteúdo no Instagram". Se a tela pedir tipo de app, escolha "Empresa".
- Se perguntar por portfólio empresarial, pode seguir sem conectar nenhum.
- Confere: ela está no painel do app novo e vê o nome dele no topo.

**2.2 Ligar o Instagram com login do Instagram**
- No menu do app: "Casos de uso" > "Personalizar" no caso do Instagram > "Configuração da API com login do Instagram". Em painéis antigos o caminho é "Adicionar produto" > Instagram > "API com login do Instagram".
- Tem que ser a opção com login do **Instagram**. A opção com login do Facebook exige Página e não serve para este modelo.
- Na lista de permissões, confira que aparecem `instagram_business_basic` e `instagram_business_content_publish`. Se a segunda não estiver, adicione.
- Confere: ela vê a seção "Gerar tokens de acesso".

**2.3 Convidar a própria conta como testadora**
- Menu do app: "Funções do app" > "Funções" > "Adicionar pessoas" > "Testador do Instagram" > digitar o handle dela > confirmar.
- Confere: o handle aparece na lista como pendente.

**2.4 Aceitar o convite**
- Logada no Instagram com a mesma conta, abrir https://www.instagram.com/accounts/manage_access/ > aba "Convites de testador" > "Aceitar".
- No aplicativo do celular o caminho é Configurações e atividade > Permissões de sites > Apps e sites > Convites de testador.
- Confere: de volta ao painel da Meta, o handle deixa de aparecer como pendente.

**2.5 Gerar o token**
- Antes de ela clicar, avise: "O token é uma senha. Não cole aqui no chat. Deixe a aba aberta, você vai colar direto no GitHub no próximo passo."
- Na seção "Gerar tokens de acesso": "Adicionar conta" > entrar com o Instagram dela > autorizar. Depois, "Gerar token" ao lado da conta > copiar.
- Esse token vale 60 dias e o repositório renova sozinho todo mês.
- O app fica em modo de desenvolvimento. Não precisa enviar para análise nem publicar o app: nesse modo ele funciona para a conta que tem função nele, que é a dela.
- Confere: ela diz que copiou o token e não colou em lugar nenhum.

Siga direto para o Passo 3, sem pausa, enquanto o token está copiado.

---

## Passo 3. Secrets no GitHub

"Secret" é um cofre do GitHub: depois de salvo, ninguém consegue ler, nem a própria pessoa. São três. O formulário é sempre o mesmo link, um secret por vez:

https://github.com/DONO/REPO/settings/secrets/actions/new

**3.1 IG_ACCESS_TOKEN**
- Name: `IG_ACCESS_TOKEN`. Secret: colar o token do Passo 2.5. Clicar em "Add secret". Clique só dela.

**3.2 GH_PAT**
- Explique em uma frase: é uma chave do GitHub que deixa o repositório trocar o token do Instagram sozinho todo mês.
- Criar em https://github.com/settings/personal-access-tokens/new (clique só dela):
  - Token name: `renovar-instagram`.
  - Expiration: a maior que a tela oferecer. Se houver "No expiration", pode usar.
  - Repository access: "Only select repositories" > escolher só este repositório.
  - Permissions > Repository permissions > "Secrets" > "Read and write".
  - "Generate token" e copiar. Também não cola no chat.
- Voltar ao formulário de secret. Name: `GH_PAT`. Secret: colar. "Add secret".
- Pergunte a data de validade que ela escolheu e peça para pôr um lembrete na agenda uma semana antes, com o texto "trocar o GH_PAT do Instagram". Anote a data em `instalacao.md`.

**3.3 IG_USER_ID**
- É o número da conta do Instagram. Não é segredo, mas fica no cofre junto com os outros.
- Para descobrir sem expor o token: rode o teste do Passo 4 agora. Ele vai falhar de propósito e mostrar a mensagem "Falta o secret IG_USER_ID. O valor certo, sem os espaços, é: ...". O número vem com espaços entre os dígitos; tire os espaços.
- Com o número em mãos, abrir o formulário de novo. Name: `IG_USER_ID`. Secret: o número, só dígitos. "Add secret".

Confere: com `gh`, `gh secret list` mostra os três nomes. Sem `gh`, a pessoa abre https://github.com/DONO/REPO/settings/secrets/actions e confirma que vê `GH_PAT`, `IG_ACCESS_TOKEN` e `IG_USER_ID`.

---

## Passo 4. Prova

**4.1 Testar a conexão**
- Com `gh`: `gh workflow run testar-conexao.yml`, depois `gh run watch` e `gh run view --log` (isso você faz).
- Sem `gh`: a pessoa abre https://github.com/DONO/REPO/actions/workflows/testar-conexao.yml > "Run workflow" > "Run workflow", espera cerca de um minuto, abre a execução e lê o resumo para você.
- Se a aba Actions mostrar um aviso pedindo para habilitar os workflows, ela clica em habilitar e roda de novo.
- Resultado esperado: **"Conexão OK"** com o @ dela.
- Se falhar, a mensagem diz o que é:
  - "Falta o secret ..." ou "não bate com o token": voltar ao Passo 3.
  - "Token inválido": o token foi copiado pela metade ou é de outro app. Refazer 2.5 e 3.1.
  - "não tem a permissão de publicar": voltar ao 2.2, adicionar `instagram_business_content_publish` e gerar o token de novo.

**4.2 Testar a renovação**
- Rode a Action "Renovar token do Instagram" do mesmo jeito (`gh workflow run renovar-token.yml`, ou o botão Run workflow na página dela).
- Esperado: "Token renovado". Depois rode o 4.1 mais uma vez para confirmar que o token novo funciona.
- Se a mensagem for "A Meta recusou a renovação" e o token acabou de ser criado, não é defeito: anote em `instalacao.md` para repetir este teste amanhã e siga.
- Se a mensagem for sobre o `GH_PAT`: refazer o 3.2. Esse é o erro que só apareceria daqui a um mês, por isso o teste é agora.

**Só declare a instalação concluída quando o 4.1 mostrar "Conexão OK".** Sem isso, diga com clareza que não terminou e qual é o passo pendente.

---

## Encerramento

Quando concluir:
1. Atualize `instalacao.md` com a data, os passos concluídos, a validade do `GH_PAT` e qualquer pendência (por exemplo, repetir o 4.2).
2. Faça commit e push do que mudou (`CLAUDE.md`, `design/`, `instalacao.md`). Antes do commit, confira que nenhum arquivo contém token.
3. Diga à pessoa, em poucas linhas:
   - como pedir o primeiro post ("faz um post sobre ...") e que nada sai sem ela dizer "publica";
   - os dois vencimentos do README: a troca do `GH_PAT` na data anotada, e que o GitHub desliga os agendamentos depois de 60 dias sem nenhum post ou commit;
   - que, se algo parar, é só pedir "testa a conexão".
4. Ofereça fazer o primeiro post de verdade agora.

A etapa 3 (acompanhar resultados) é opcional e ainda não existe. Só mencione se a pessoa perguntar: a proposta está em `docs/etapa-3-acompanhamento.md`.
