# 📊 Sales ETL Pipeline — Data Quality & Consolidation

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/ETL-Pipeline-orange)
![Status](https://img.shields.io/badge/Status-Concluído-brightgreen)
![Licença](https://img.shields.io/badge/Licença-MIT-lightgrey)

Pipeline de ingestão, limpeza e validação de dados de vendas construído em Python puro (sem dependências externas). O projeto simula um ambiente real de varejo, aplicando **Quality Gates** para garantir a integridade dos dados antes da camada analítica.

---

## 🧩 O Problema de Negócio

Bases de dados transacionais acumulam inconsistências com frequência: preços negativos, quantidades inválidas, strings com espaços extras, campos nulos e registros duplicados com grafias diferentes. Esses erros tornam impossível gerar relatórios financeiros confiáveis.

Este pipeline resolve exatamente isso — transformando dados brutos e desestruturados em um dataset limpo, padronizado e pronto para consumo por ferramentas de BI.

---

## ⚙️ Como o Pipeline Funciona

```
Raw Data (12 registros)
        │
        ▼
┌─────────────────────┐
│  1. Ingestão        │  Extração dos registros brutos do sistema transacional
└─────────────────────┘
        │
        ▼
┌─────────────────────┐
│  2. Data Cleaning   │  Normalização de strings, trim de whitespace, Title Case
└─────────────────────┘
        │
        ▼
┌─────────────────────┐
│  3. Quality Gates   │  Validação de regras de negócio (preço, quantidade, campos obrigatórios)
└─────────────────────┘
        │
        ├──────────────────────────────────┐
        ▼                                  ▼
┌──────────────┐                  ┌─────────────────┐
│ vendas_valid │                  │ vendas_invalidas │
│ (6 registros)│                  │ (6 registros)    │
└──────────────┘                  └─────────────────┘
        │
        ▼
┌─────────────────────┐
│  4. Data Quality    │  Relatório final com métricas de qualidade e análise financeira
│     Report          │
└─────────────────────┘
```

---

## 📋 Regras de Negócio Aplicadas (Quality Gates)

| Regra | Critério | Ação se violada |
|---|---|---|
| Preço válido | `preco > 0` | Registro rejeitado |
| Quantidade válida | `1 ≤ quantidade ≤ 100` | Registro rejeitado |
| Produto não nulo | Campo não pode ser vazio | Registro rejeitado |
| Vendedor não nulo | Campo não pode ser vazio | Registro rejeitado |

---

## 📈 Resultados do Pipeline

```
DATA QUALITY REPORT — SALES ETL PIPELINE
Tech Shop | Consolidação de Vendas do Período
════════════════════════════════════════════

Registros Recebidos (Raw):   12
Registros Aprovados:          6  (50.0%)
Registros Rejeitados:         6  (50.0%)

ANÁLISE FINANCEIRA CONSOLIDADA
Faturamento Total (válido):  R$ 2.965,00
Produto mais vendido:        mouse gamer (3 transações)

RANKING DE PRODUTOS
  1º mouse gamer      → 3 transações
  2º teclado mecânico → 1 transação
  3º webcam           → 1 transação
  4º ssd 480gb        → 1 transação
```

---

## 🔍 Tipos de Anomalias Detectadas

O dataset bruto continha intencionalmente os seguintes erros — todos identificados e tratados pelo pipeline:

- **Preço negativo** → `"TECLADO MECANICO": preco = -150.00`
- **Preço zerado** → `"webcam": preco = 0`
- **Quantidade zero** → `"Monitor LG": quantidade = 0`
- **Whitespace em strings** → `"  MARIA SILVA  "` → normalizado para `"Maria Silva"`
- **Case inconsistente** → `"MOUSE GAMER"`, `"Mouse Gamer"`, `"mouse gamer"` → todos normalizados para `"mouse gamer"`
- **Campos nulos** → vendedor ou produto em branco

---

## 🗂️ Estrutura do Projeto

```
retail-data-cleaner/
│
├── Sales_ETL_Pipeline.ipynb   # Notebook principal com o pipeline completo
├── README.md                  # Documentação do projeto
├── .gitignore
└── LICENSE
```

---

## ▶️ Como Executar

**Pré-requisitos:** Python 3.10+ (sem bibliotecas externas — stdlib only)

```bash
# Clone o repositório
git clone https://github.com/JoaoVitor1110/retail-data-cleaner.git
cd retail-data-cleaner

# Abra o notebook
jupyter notebook Sales_ETL_Pipeline.ipynb
```

Execute as células em ordem. O relatório final é gerado automaticamente na última célula.

---

## 🛠️ Stack Utilizada

- **Python 3** — lógica do pipeline (stdlib only, sem dependências)
- **Jupyter Notebook** — ambiente de desenvolvimento e documentação
- **Estruturas nativas** — listas, dicionários, funções e controle de fluxo

---

## 👤 Autor

**João Vitor Alves** — Analista de Dados Jr. | Python · SQL · Power BI · n8n

[![LinkedIn](https://img.shields.io/badge/LinkedIn-jvs--alves-blue?logo=linkedin)](https://linkedin.com/in/jvs-alves)
[![Portfólio](https://img.shields.io/badge/Portfólio-jvsatech.com.br-informational)](https://portfolio.jvsatech.com.br)
