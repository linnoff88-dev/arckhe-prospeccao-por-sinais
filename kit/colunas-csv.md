# Colunas do CSV de saída

Arquivo: `saida/leads-AAAA-MM-DD.csv`, UTF-8, separado por vírgula, uma linha por decisor.
As colunas vêm nesta ordem. **Obrigatória** = não pode ficar em branco.

| # | coluna | obrigatória | o que vai | exemplo (fictício) |
|---|--------|-------------|-----------|--------------------|
| 1 | `empresa` | sim | nome da empresa | Exemplo Software Ltda. |
| 2 | `site` | sim | domínio principal | exemplosoftware.com.br |
| 3 | `cidade` | sim | cidade / UF | Recife, PE |
| 4 | `funcionarios` | sim | faixa de funcionários | 201-500 |
| 5 | `decisor` | sim | nome completo | Paula Andrade |
| 6 | `cargo` | sim | cargo atual | Diretora de Operações |
| 7 | `email` | sim | e-mail profissional | paula@exemplosoftware.com.br |
| 8 | `email_status` | sim | verificado / arriscado / não encontrado | verificado |
| 9 | `fonte_email` | sim | fornecedor da cascata que achou o e-mail | (nome do fornecedor) |
| 10 | `telefone` | não | só se pedido; não sai no grátis/teste | |
| 11 | `sinal` | sim | `id` do sinal em `sinais.yaml` | contratacao_ia |
| 12 | `data_sinal` | sim | data do evento (AAAA-MM-DD) | 2026-10-20 |
| 13 | `resumo_sinal` | sim | 1 frase sobre o que aconteceu | Abriu vaga de engenheira de IA em São Paulo |
| 14 | `link_fonte_sinal` | sim | URL onde o sinal foi visto | https://exemplosoftware.com.br/carreiras/123 |
| 15 | `gancho` | sim | ligação entre o sinal e a oferta (1 frase) | vaga de IA costuma vir junto com fila de suporte crescendo |
| 16 | `assunto` | sim | até 6 palavras | a vaga de engenheira de IA |
| 17 | `corpo` | sim | até 90 palavras, com sinal, CTA leve e opt-out | Oi, Paula, vi que... |
| 18 | `revisar` | sim | sim / não | não |
| 19 | `motivo_revisao` | se `revisar = sim` | por que precisa de olho humano | sinal com 40 dias (perto do fim da janela) |

## Regras de conferência

- `email_status` diferente de `verificado` → a linha sai do CSV final (ou vai para revisão, se você preferir).
- `data_sinal` fora da `janela_dias` do sinal → a linha sai.
- `corpo` sem a linha de saída → refazer.
- Guarde o CSV: as colunas `link_fonte_sinal` e `fonte_email` são o registro de **origem do dado** (LGPD).
