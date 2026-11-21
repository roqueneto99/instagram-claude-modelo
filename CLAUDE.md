# Instruções para o Claude neste repositório

Este repositório publica no Instagram do dono dele. Publicar é público e não tem volta.

Se a Parte 2 ainda tiver campos com `PREENCHER`, a instalação não terminou: avise a pessoa e sugira rodar `/instalar` antes de criar qualquer post.

---

## Parte 1. Regras fixas (não mudam)

1. **Nada publica sem o "publica" da pessoa para aquele post.** Só mude um `post.json` para `"status": "aprovado"` quando a pessoa disser, no chat e sobre aquele post específico, que é para publicar. A aprovação de um post não vale para outro. Aprovar o visual não é mandar publicar. Na dúvida, deixe `rascunho` e pergunte.
2. **Nunca grave token ou senha em arquivo.** Token só existe nos secrets do GitHub. Não peça para a pessoa colar token no chat. Se ela colar, avise que aquele token deve ser descartado e gerado de novo.
3. **Nunca reenvie post publicado.** Não altere um `post.json` com status `publicado` ou `publicando`. Para corrigir um post que já saiu, a pessoa edita ou apaga no próprio Instagram.
4. **Erro não se repete sozinho.** Se o status for `erro`, explique o campo `erro` em linguagem simples e só volte para `aprovado` com o ok da pessoa.
5. **Mostre antes.** Toda arte e toda legenda aparecem no chat antes de qualquer commit.

### Como um post nasce e sai

1. Monte a arte seguindo a Parte 2 e trabalhe na pasta `rascunhos/` (ela não vai para o GitHub). Abra o PNG gerado e confira com os próprios olhos antes de mostrar.
2. Mostre os PNGs e a legenda no chat. Ajuste até a pessoa aprovar.
3. Depois do "publica":
   - imagens: `python scripts/preparar_post.py <slug> legenda.txt img1.png img2.png ...` (precisa do Pillow: `pip install pillow`). O script converte para JPEG 1080x1350 e cria `posts/<data>-<slug>/post.json` como `rascunho`.
   - vídeo (Reels): copie o MP4 vertical para `posts/<data>-<slug>/video.mp4` (H.264 com áudio AAC, abaixo de 19 MB) e use `"video": "video.mp4"` no lugar de `imagens`. Opcional: `"capa_ms": 3000` escolhe o quadro da capa.
   - mude o status para `aprovado`. Se a pessoa pediu horário, acrescente `"agendado_para"` com data, hora e fuso, por exemplo `"2030-01-15T09:00:00-03:00"`.
   - confira: 1 a 10 imagens, legenda com até 2.200 caracteres e até 30 hashtags, nada da lista "nunca escrever" da Parte 2.
   - commit `post: <slug>` e push na `main`. A publicação só dispara na `main`.
4. Acompanhe a Action "Publicar no Instagram" (`gh run watch`, ou a aba Actions do repositório).
5. `git pull` e leia o `post.json`. Se `publicado`, entregue o `link` à pessoa. Se `erro`, siga a regra 4.

### Formato do post.json

```json
{
  "status": "rascunho",
  "imagens": ["01.jpg", "02.jpg"],
  "legenda": "Texto da legenda com #hashtags"
}
```

Status: `rascunho`, `aprovado`, `publicando`, `publicado`, `erro`. A Action acrescenta sozinha `media_id`, `link`, `publicado_em` e, quando falha, `erro`.

Post agendado depende do relógio do GitHub, que pode atrasar de minutos a algumas horas. Para hora exata, publique na hora, sem `agendado_para`.

### Quando algo parar de funcionar

- Rode a Action "Testar conexão com o Instagram". Ela diz se o problema é o token.
- Token vencido: gerar outro no painel da Meta e trocar o secret `IG_ACCESS_TOKEN` (Passo 2 e Passo 3 do `/instalar`).
- "Renovar token do Instagram" falhando: quase sempre é o `GH_PAT` vencido. Criar outro e trocar o secret.
- Nada roda há semanas: o GitHub desliga os agendamentos de repositório público depois de 60 dias sem commit. Reative na aba Actions.

---

## Parte 2. Design system (preenchido no /instalar)

> Enquanto houver `PREENCHER` abaixo, o design system está incompleto.

### Perfil
- Handle: PREENCHER
- Sobre o que é o perfil, em uma frase: PREENCHER
- Para quem fala: PREENCHER
- Idioma: PREENCHER

### Cores
- Fundo principal: PREENCHER (código hexadecimal)
- Texto principal: PREENCHER
- Cor de destaque: PREENCHER
- Cor secundária (opcional): PREENCHER
- Quando usar cada uma: PREENCHER

### Fontes
- Títulos: PREENCHER (nome da fonte e peso)
- Texto corrido: PREENCHER
- De onde vêm (Google Fonts ou arquivo em `design/fontes/`): PREENCHER

### Tom de voz
- Como o perfil fala: PREENCHER
- Três frases de exemplo no tom certo: PREENCHER
- Emoji: PREENCHER (usa, usa pouco, não usa)
- Chamada final de costume: PREENCHER

### Formatos
Tamanho padrão: 1080 x 1350 pixels.

**Post único**
- Estrutura (o que vai no topo, no meio e no rodapé): PREENCHER
- Tamanho do título e limite de palavras na arte: PREENCHER
- Arquivo base: PREENCHER (por exemplo `design/base-post.html`)

**Carrossel**
- Quantidade de telas de costume e máximo: PREENCHER
- Capa: PREENCHER
- Telas do meio: PREENCHER
- Última tela: PREENCHER
- Arquivo base: PREENCHER (por exemplo `design/base-carrossel.html`)

### Assinatura
- O que aparece em toda arte (handle, site, logo): PREENCHER
- Logo: PREENCHER (caminho do arquivo em `design/`, ou "não tem")

### Legenda
- Tamanho de costume: PREENCHER
- Hashtags fixas: PREENCHER

### O que nunca escrever
- PREENCHER (palavras, promessas, assuntos e sinais de pontuação proibidos)

### Como gerar a arte
- Método que funcionou neste computador: PREENCHER (por exemplo: HTML renderizado em PNG pelo Chrome sem janela)
- Comando de render: PREENCHER
