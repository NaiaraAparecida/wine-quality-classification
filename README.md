# 🍷 Wine Quality Classification

Classificação da qualidade de vinhos com Machine Learning — **Tech Challenge Fase 2** da pós-graduação em Data Analytics (FIAP).

---

## 📌 Objetivo

Desenvolver um modelo de **classificação** capaz de prever a qualidade de um vinho a partir de suas características físico-químicas, apoiando enólogos e produtores na padronização da qualidade.

A nota de qualidade original (de 3 a 8) foi transformada em uma variável **binária**:

- **Alta qualidade**: nota ≥ 7 → `1`
- **Baixa/Média qualidade**: nota < 7 → `0`

---

## 📊 Sobre o dataset

Base **Wine Quality Dataset** (Kaggle: `yasserh/wine-quality-dataset`), com **1.143 amostras** e 11 variáveis físico-químicas:

| Variável | Descrição |
|---|---|
| fixed acidity | Acidez fixa |
| volatile acidity | Acidez volátil |
| citric acid | Ácido cítrico |
| residual sugar | Açúcar residual |
| chlorides | Cloretos |
| free sulfur dioxide | Dióxido de enxofre livre |
| total sulfur dioxide | Dióxido de enxofre total |
| density | Densidade |
| pH | pH |
| sulphates | Sulfatos |
| alcohol | Teor alcoólico |
| quality | Nota de qualidade (variável de origem do alvo) |

> A coluna `Id` foi removida por ser apenas um identificador, sem relação com a qualidade.

---

## 📁 Estrutura do repositório

```
wine-quality-classification/
├── data/              # Base de dados utilizada (WineQT.csv)
├── notebooks/         # Notebook com a análise e modelagem
├── src/               # Scripts auxiliares (pré-processamento / modelagem)
├── results/           # Gráficos, métricas e relatório de resultados
├── requirements.txt   # Bibliotecas utilizadas
└── README.md          # Descrição do projeto
```

---

## ⚙️ Como executar

1. Clone o repositório:
   ```bash
   git clone https://github.com/<usuario>/wine-quality-classification.git
   cd wine-quality-classification
   ```
2. Instale as dependências:
   ```bash
   pip install -r requirements.txt
   ```
3. Abra o notebook em `notebooks/` e execute as células na ordem. A base é lida localmente de `data/WineQT.csv`.

---

## 🔎 Etapas do projeto

1. **Compreensão do problema** — definição do alvo e transformação binária (≥ 7).
2. **Análise Exploratória (EDA)** — distribuições, correlações, outliers e balanceamento das classes.
3. **Pré-processamento** — verificação de nulos e duplicatas, divisão treino/teste estratificada e padronização (`StandardScaler`).
4. **Modelagem** — treino e comparação de três modelos de classificação.
5. **Avaliação** — métricas adequadas ao desbalanceamento (precisão, recall, F1 e ROC-AUC).
6. **Interpretação** — variáveis de maior influência na qualidade e implicações para a produção.

---

## 📈 Principais resultados

### Qualidade dos dados
- **Sem valores faltantes**.
- **125 registros duplicados** identificados e avaliados na análise.

### Balanceamento das classes
As classes são **fortemente desbalanceadas** (~86% baixa/média vs ~14% alta qualidade). Por isso foram usadas métricas além da acurácia e o parâmetro `class_weight="balanced"`.

### Desempenho dos modelos (classe 1 — alta qualidade)

| Modelo | Precisão | Recall | F1-score | ROC-AUC |
|---|---|---|---|---|
| Regressão Logística | 0,38 | 0,69 | 0,49 | 0,85 |
| **Random Forest** | **0,80** | 0,50 | **0,62** | **0,90** |
| Gradient Boosting | 0,67 | 0,56 | 0,61 | 0,88 |

- A **Regressão Logística** tem alto recall e baixa precisão (encontra vinhos bons, mas gera alarmes falsos).
- O **Random Forest** tem o melhor equilíbrio geral e o maior ROC-AUC, sendo o **modelo recomendado**.
- A escolha final depende do objetivo de negócio: priorizar **recall** (não perder vinhos bons) ou **precisão** (confiar na indicação de "alta qualidade").

### Variáveis mais influentes
De acordo com a importância do Random Forest e a análise de correlação:

- **alcohol (teor alcoólico)** — fator mais associado à qualidade.
- **sulphates**, **volatile acidity** e **citric acid** — contribuições relevantes.

**Implicação para a produção:** como o teor alcoólico (definido na fermentação) é o principal determinante, o controle da fermentação surge como ponto-chave para elevar e padronizar a qualidade.

---

## 🛠️ Tecnologias

Python · pandas · numpy · matplotlib · seaborn · scikit-learn

---

## 👥 Equipe

| Nome | RM |
|---|---|
| Alecsander Victorino da Silva | RM376343 |
| Ana Julia Paiva Gomes | RM376348 |
| Priscila Jardim Donega | RM376722 |
| Naiara Cruz | RM375977 |

---

## 📎 Entregáveis

| Entregável | Link |
|---|---|
| Repositório (código) | Este repositório |
| Relatório Executivo | https://1drv.ms/w/c/d6ce280d686b6ca1/IQBqJF_pmD-5Sri0_OOiHW7sATAahrnbPqu21PurQySTD0w?e=GrJf96 |
| Apresentação | https://docs.google.com/presentation/d/1CqaVUv0SDeUk7jDp4Qo644ylC_7mpG8IbliOqamzOGE/edit?usp=sharing |
| Vídeo (5 min) | https://www.youtube.com/watch?v=x6ygUTEjToc |
