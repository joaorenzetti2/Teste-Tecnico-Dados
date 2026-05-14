# 🏗️ Projeto de Business Intelligence  
## Análise Financeira e Operacional da ConstruData (2025–2026)

## 📌 Visão Geral do Projeto

Este projeto consiste no desenvolvimento de um dashboard estratégico no Power BI para a construtora fictícia **ConstruData S.A.**, com foco em responder perguntas críticas relacionadas a:

- Faturamento
- Gestão de custos
- Eficiência operacional
- Controle financeiro
- Indicadores estratégicos (KPIs)

A solução contempla todo o fluxo de dados, desde a extração e tratamento (ETL) até a modelagem dimensional e construção de métricas DAX.

---

# ⚙️ Tratamento e Engenharia de Dados (ETL)

Durante o processo de transformação dos dados no Power Query, foram aplicadas diversas boas práticas para garantir consistência e qualidade analítica.

## 🔹 Padronização de Chaves

Aplicação das funções:

```powerquery
Text.Trim()
Text.Upper()
```

Objetivo:

- Remover espaços extras
- Padronizar IDs e códigos
- Evitar falhas de relacionamento

---

## 🔹 Tratamento de Inconsistências

Criação de um registro padrão:

```text
DESCONHECIDO
```

Utilizado para fornecedores não cadastrados, evitando perda de registros na tabela fato.

---

## 🔹 Tipagem de Dados

Configuração rigorosa dos tipos de dados financeiros:

- Número Decimal
- Localidade PT-BR

Objetivo:

- Evitar erros de separador decimal
- Garantir precisão nos cálculos financeiros

---

# 🧩 Modelagem de Dados — Star Schema

A modelagem foi construída seguindo o padrão **Star Schema**, visando:

- Melhor performance
- Facilidade de manutenção
- Escalabilidade
- Maior clareza analítica

## 📌 Tabelas Fato

- `f_Lancamentos_Financeiros`
- `f_Notas_Fiscais`

## 📌 Tabelas Dimensão

- `d_Calendario`
- `d_Fornecedores`
- `d_Plano_de_Contas`
- `d_Centro_Custo`

## 📌 Relacionamentos

- Relacionamentos `1:N`
- Propagação de filtro unidirecional

---

# 📊 Inteligência de Negócio (DAX)

## 📌 Cálculo do PMP (Prazo Médio de Pagamento)

```DAX
PMP Ponderado = 
VAR SomaPonderada =
    SUMX(
        f_Notas_Fiscais,
        [Dias_Prazo] * f_Notas_Fiscais[Valor_NF]
    )

VAR SomaValores =
    SUM(f_Notas_Fiscais[Valor_NF])

RETURN
    DIVIDE(SomaPonderada, SomaValores)
```

---

## 📌 Outras Medidas Principais

### Total Receita

```DAX
Total Receita =
CALCULATE(
    SUM(Lancamentos[Valor]),
    Plano_de_Contas[Categoria] = "Receita"
)
```

---

### Total Despesa

```DAX
Total Despesa =
CALCULATE(
    SUM(Lancamentos[Valor]),
    Plano_de_Contas[Categoria] = "Despesa"
)
```

---

### Notas em Atraso

```DAX
Notas em Atraso =
-- Contagem filtrada de notas com status "Atraso"
```

---

# 📈 O Dashboard

## 🔹 Cards de Resumo (Top Row)

| KPI | Objetivo |
|---|---|
| **Total Receita** | Visão imediata do faturamento bruto |
| **Total Despesa** | Controle de saídas e custos operacionais |
| **PMP Geral** | Média de dias de prazo com fornecedores |
| **Volume de Notas** | Intensidade da operação logística |

---

# 📉 Detalhamento dos Gráficos

## 📌 Gráfico 1 e 2 — Top Planos

Identificam quais contas geraram:

- Maior receita
- Maior despesa

📅 Referência: **Janeiro/2025**

---

## 📌 Gráfico 3 — Ranking PMP

Exibe os fornecedores que oferecem os melhores prazos médios de pagamento em 2026.

---

## 📌 Gráfico 4 — Centro de Custo

Treemap com distribuição das despesas por obra/projeto.

📅 Referência: **2025**

---

## 📌 Gráfico 5 — Status das Notas

Gráfico de rosca para monitoramento de:

- Notas pagas
- Notas atrasadas

---

## 📌 Gráfico 6 — Segmentos de Fornecedores

Mostra a concentração de gastos por nicho/segmento de fornecedor.

---

## 📌 Gráfico 7 — Atrasos por UF

Mapa geográfico demonstrando os principais riscos de inadimplência por estado.

---

## 📌 Gráfico 8 — Evolução Financeira

Linha do tempo comparativa entre:

- Receita
- Despesa

📅 Referência: **2025**

---
# Dashboard:

<img width="1535" height="863" alt="dashteste" src="https://github.com/user-attachments/assets/c354d7ac-49f8-47ed-8798-0c83c68bcc27" />

