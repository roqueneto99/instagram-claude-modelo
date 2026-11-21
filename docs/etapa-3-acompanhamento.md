# Etapa 3 (opcional): acompanhar resultados

Proposta de uma página. Nada disto está construído. Serve para decidir se vale fazer.

## O que seria

Uma quarta Action, "Ler desempenho dos posts", que lê as métricas dos últimos posts pela mesma API e pelo mesmo token da publicação. Sem servidor, sem banco e sem custo.

Uso no dia a dia: você pergunta ao Claude "como foram os posts do mês?", ele roda a Action, lê o resultado e responde em texto.

## O que responderia

1. Quais posts alcançaram mais gente e quais foram mais salvos e compartilhados.
2. Qual formato rende mais para o seu perfil: post único, carrossel ou Reels.
3. O que repetir e o que largar, comparando com os seus posts anteriores.

Métricas por post: alcance, visualizações, salvamentos, compartilhamentos, curtidas, comentários, novos seguidores e visitas ao perfil.

## O que precisa

- Uma permissão a mais no app da Meta: `instagram_business_manage_insights`. Depois de adicionar, gerar o token de novo e trocar o secret `IG_ACCESS_TOKEN`.
- Um script de leitura (`scripts/insights.py`) e um workflow manual. Cerca de 100 linhas no total.
- Um comando `/resultados` para o Claude rodar, ler e resumir.

## O que fica de fora da versão simples

- **Anúncios pagos** (gasto, custo por resultado, campanhas). Isso usa outra API, outro token e uma conta de anúncios. É um projeto separado e só faz sentido para quem anuncia toda semana.
- Histórico longo e painel com gráficos. A versão simples lê na hora e responde no chat. Se um dia fizer falta, o passo seguinte é gravar um arquivo por semana em `relatorios/`.
- Métricas de posts com mais de dois anos, de Stories já expirados e de contas com menos de 100 seguidores em alguns recortes: a Meta não entrega.

## Esforço e risco

- Para construir: uma tarde.
- Para quem instala: 10 minutos (adicionar a permissão e trocar o token).
- Risco: baixo. É só leitura e não publica nada.

## Decisão pendente

Construir só se pelo menos duas pessoas que instalaram o modelo pedirem. Antes disso, o próprio aplicativo do Instagram mostra esses números.
