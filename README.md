# 📊 Projeto Power BI – Modelo em Estrela com Financial Sample

Este projeto foi desenvolvido como parte do curso **Klabin - Excel e Power BI Dashboards**, promovido pela **DIO (Digital Innovation One)**.

O objetivo foi transformar uma única tabela de dados financeiros em um modelo analítico dimensional, utilizando **DAX**, **Power BI** e a metodologia de modelagem em **Esquema Estrela (Star Schema)**.

---

## 🧱 Estrutura do Projeto

A estrutura do modelo segue o padrão de **Data Warehouse**, com separação clara entre:

- Tabela Fato (`f_vendas`)
- Tabelas Dimensão (`d_produtos`, `d_detalhes`, etc.)
- Tabela de Datas (`calendario`)

---

## 🌟 Esquema Estrela

Abaixo está a representação visual do modelo:

> Os relacionamentos foram estabelecidos no formato 1:* (um para muitos), com as dimensões ligadas à tabela fato `f_vendas`.

---

## 📁 Tabelas Criadas

### 🔹 Tabela Fato: `f_vendas`

Contém os dados transacionais de vendas, como:

- ID Produto
- Produto
- Unidades Vendidas
- Preço de Venda
- Faixa de Desconto
- Segmento
- País
- Vendedor
- Lucro
- Data

---

### 🔸 Tabelas Dimensão

| Tabela                | Descrição |
|------------------------|-----------|
| `d_produtos`           | Informações dos produtos e métricas como média, mediana, valor máx./mín. |
| `d_produtos_detalhes`  | Detalhes adicionais: Discount Band, Sale Price, Units Sold, etc. |
| `d_descontos`          | Faixa de descontos por produto. |
| `d_detalhes`           | Métricas como Sales, Gross Sales, Profit, etc. |
| `d_categorias`         | Dados categóricos como região, país e segmento. |
| `calendario`           | Tabela de datas criada via DAX. |
| `financials_origem`    | Tabela original importada (modo oculto, usada como base). |

---

## 📅 Tabela Calendário (DAX)

A tabela `calendario` foi criada para dar suporte a análises temporais (por ano, mês, dia da semana, etc.) e foi marcada como **Tabela de Datas** no Power BI.

### 📌 Código DAX Utilizado:

```DAX
Calendario = 
ADDCOLUMNS(
    CALENDAR(DATE(2015, 01, 01), DATE(2030, 12, 31)),
    "Ano", YEAR([Date]),
    "Ano-Mês", FORMAT([Date], "YYYY-MM"),
    "Mês", FORMAT([Date], "MMMM"),
    "Número do Mês", MONTH([Date]),
    "Dia", DAY([Date]),
    "Dia da Semana", FORMAT([Date], "dddd"),
    "Número do Dia da Semana", WEEKDAY([Date], 2)
)
```

---

## ⚙️ Funções DAX Utilizadas no Projeto

O projeto utilizou uma variedade de funções DAX, tanto para criar colunas calculadas quanto medidas nas tabelas dimensão e fato:

### 📆 Manipulação de Datas
- `CALENDAR()` – Cria uma tabela com intervalo de datas.
- `CALENDARAUTO()` – (alternativa usada em testes) cria calendário baseado nas datas do modelo.
- `YEAR([Date])` – Extrai o ano de uma data.
- `MONTH([Date])` – Extrai o número do mês.
- `FORMAT([Date], "MMMM")` – Retorna o nome do mês.
- `DAY([Date])` – Retorna o número do dia.
- `WEEKDAY([Date], 2)` – Retorna o número do dia da semana (2 = Segunda a Domingo).
- `FORMAT([Date], "dddd")` – Nome completo do dia da semana.
- `FORMAT([Date], "YYYY-MM")` – Formata como ano-mês.

### 📊 Agregações e Métricas (nas dimensões)
- `AVERAGEX()` – Média baseada em expressão dentro de uma tabela.
- `MEDIANX()` – Mediana baseada em expressão.
- `MINX()`, `MAXX()` – Mínimo e máximo de uma expressão.
- `CALCULATE()` – Avaliação de uma expressão com contexto modificado.
- `SUMMARIZE()` – Agrupamento de dados por colunas específicas.
- `GROUPBY()` – Alternativa ao `SUMMARIZE`, com suporte a cálculos inline.

---

## 🧪 Recursos Utilizados

- **Power BI Desktop**
- **DAX (Data Analysis Expressions)**
- **Modelagem Dimensional**
- **Ferramenta de Relacionamentos do Power BI**
- **Painéis e Visualizações**

---

## 📂 Arquivos Incluídos

- `projeto.pbix` – Arquivo do Power BI com o modelo completo.
- `schema.png` – Imagem do modelo dimensional.
- `README.md` – Este documento de explicação.

---

## ✅ Conclusão

Este projeto mostra a transformação de uma única tabela de dados em um modelo analítico bem estruturado, com clara separação de responsabilidades e aproveitamento total das funcionalidades do Power BI e DAX.

A criação de um **modelo em estrela** garante:
- Melhor desempenho
- Facilidade de uso por analistas
- Escalabilidade para novos dados
- Análises temporais avançadas com uso da tabela calendário

---

## 👨‍🎓 Curso de Origem

Este projeto foi desenvolvido como parte do curso:

> **Klabin - Excel e Power BI Dashboards**, promovido pela **[DIO - Digital Innovation One](https://www.dio.me/)**.

---
