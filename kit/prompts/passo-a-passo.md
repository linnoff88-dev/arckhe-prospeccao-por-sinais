# Os 7 passos em linguagem natural

Use estes prompts no Claude Code, um de cada vez, quando quiser controlar cada etapa (em vez de
um `/goal` só). Cada prompt já pede o teste de 10 linhas e a confirmação antes de gastar crédito.

---

## Passo 1 — ICP: a lista de empresas

```text
Leia contexto/perfil-do-negocio.md. Pelo Clay, monte uma tabela de empresas do nosso ICP:
setor <software>, <200 a 1.000> funcionários, país <Brasil>. Inclua site, cidade, número de
funcionários e LinkedIn da empresa. Rode 10 linhas, me mostre e diga quanto custaria rodar
<200> empresas. Não rode o resto sem eu dizer "pode".
```

## Passo 2 — Sinal de contratação monitorado

```text
Para as empresas da tabela, configure no Clay o monitoramento de vagas abertas com estes cargos
ou palavras: <engenheiro de IA, automação, machine learning>. Use a janela de
validade do sinal "contratacao_ia" em sinais.yaml. Para cada empresa, quero: contratacao_ia
(sim/não), título da vaga, data e link. Teste em 10 empresas primeiro.
```

## Passo 3 — Agente de pesquisa: lançamento de produto

```text
Adicione uma coluna de agente de IA que pesquisa se a empresa anunciou produto ou recurso de IA
nos últimos <90> dias (site, blog, notícias, página de novidades). Saída em campos separados:
encontrou (sim/não), o que lançou (1 frase), data, link da fonte. Se não achar fonte, a resposta
é "não" — não deduza. Rode 10 linhas e me mostre antes do resto.
```

## Passo 4 — Decisor só onde há sinal

```text
Calcule, para cada empresa, a soma dos pesos dos sinais ativos (sinais.yaml, dentro da janela).
Busque pessoas com os cargos <diretor(a) de operações, diretor(a) de suporte/CS, CTO>, mas só nas
empresas com soma >= 30 ("empresa com sinal"). As outras ficam de fora e não gastam crédito. Mande os decisores para uma tabela nova. Teste em 10 empresas.
```

## Passo 5 — Enriquecimento em cascata

```text
Para cada decisor, encontre o e-mail profissional em cascata (vários fornecedores em sequência,
parando no primeiro e-mail válido) e verifique o e-mail. Telefone: <não> buscar. Marque
email_status como verificado, arriscado ou não encontrado. Rode 10 linhas e me diga a taxa de
acerto antes de seguir.
```

## Passo 6 — Mensagem com contexto

```text
Leia contexto/ inteiro. Para cada decisor com e-mail verificado, escreva assunto (até 6
palavras) e corpo (até 90 palavras) no tom de contexto/tom-de-voz.md. Abra pelo sinal daquela
empresa, conecte com um caso de contexto/casos.md quando fizer sentido, termine com uma pergunta
simples e a linha de saída. Não afirme nada que não esteja em contexto/provas.md. Marque
revisar = sim quando tiver dúvida e diga o motivo. Mostre 5 exemplos antes de escrever o resto.
```

## Passo 7 — Revisão humana e sequenciador

```text
Gere saida/leads-<AAAA-MM-DD>.csv com as colunas de colunas-csv.md. Confira: nenhuma célula
obrigatória em branco, todo e-mail verificado, toda mensagem com sinal e opt-out. Liste as
linhas com revisar = sim. Não envie nada.
```

Depois, **você** (não o agente):

1. Abre o CSV, lê as mensagens marcadas e corrige o que precisar.
2. Importa o CSV no sequenciador (no Clay: importar dados → CSV → nova tabela → campanha).
3. Envia de um **domínio secundário aquecido**, com poucos envios por dia e aumento gradual.
4. Acompanha a taxa de spam: o Gmail pede que fique abaixo de 0,3%.
5. Quem responder "sair" vai para `supressao.csv` na hora.
