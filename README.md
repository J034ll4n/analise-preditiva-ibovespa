# Modelagem Preditiva para Classificação de Tendência do IBOVESPA | Acurácia Final: 80%

![Status: Concluído](https://img.shields.io/badge/Status-Concluído-brightgreen)
![Acurácia](https://img.shields.io/badge/Acurácia_Final-80%25-success)
![Linguagem](https://img.shields.io/badge/Linguagem-Python_3-blue)
![Bibliotecas](https://img.shields.io/badge/Bibliotecas-Scikit--learn_|_XGBoost_|_Pandas-lightgrey)

## 1. Introdução e Objetivo do Projeto

O objetivo deste projeto foi desenvolver um modelo preditivo para prever a tendência de fechamento (**alta** ou **baixa**) do índice IBOVESPA para o dia seguinte. Este modelo servirá como um insumo para dashboards internos, auxiliando analistas quantitativos na tomada de decisão.

Para isso, foi utilizada a base de dados histórica do IBOVESPA, com granularidade diária, abrangendo um período extenso (2005-2025) para garantir a robustez e a capacidade de generalização do modelo.

---

## 2. Exploração, Limpeza e Padronização dos Dados

A primeira etapa consistiu no tratamento dos dados brutos para torná-los utilizáveis. O processo incluiu a conversão de tipos de dados, a padronização de valores de volume e a ordenação cronológica da série, resultando em um dataset limpo para a fase de análise.

---

## 3. Análise Exploratória dos Dados (EDA)

Uma análise detalhada foi realizada para extrair insights e entender o comportamento do IBOVESPA ao longo do tempo.

#### Gráfico da Série Histórica
A história do índice é marcada por ciclos e eventos macroeconômicos. Um modelo preditivo precisa ser treinado com um longo histórico para aprender com esses diferentes "regimes" de mercado.
![Gráfico da Série Histórica](img/download%20(27).png)

#### Distribuição e Densidade do Preço
A análise de densidade revela que o IBOVESPA operou historicamente em dois "regimes" de preço principais, em torno de 60.000 e 115.000 pontos, em vez de se concentrar em uma única média.

| Boxplot do Preço de Fechamento | Gráfico de Violino (Densidade) |
| :---: | :---: |
| ![Boxplot](img/download%20(28).png) | ![Gráfico de Violino](img/download%20(29).png) |

#### Análise do Volume de Negociações
O gráfico de volume revela uma quebra estrutural em 2008, mostrando que a crise não afetou apenas o preço, mas alterou fundamentalmente a liquidez do mercado.
![Gráfico de Volume](img/download%20(30).png)

#### Análise de Tendência com Médias Móveis
A posição do preço em relação às médias móveis é um indicador claro da tendência principal do mercado (bull vs. bear market) e as próprias médias atuam como suportes e resistências dinâmicos.
![Médias Móveis](img/download%20(31).png)

---

## 4. Modelagem Preditiva: A Mudança de Estratégia

A abordagem inicial focou em modelos de série temporal clássicos. A decomposição da série e o teste Augmented Dickey-Fuller (ADF) confirmaram que o IBOVESPA é uma série **não-estacionária**, um desafio para modelos como o ARIMA.

| Decomposição da Série | Série Estacionária (Pós-Tratamento) |
| :---: | :---: |
| *A forte tendência mostra que a série não é estacionária.* | *Somente após transformações a série se torna previsível.* |
| ![Decomposição da Série](img/download%20(41).png) | ![Série Detrended e Diferenciada](img/download%20(42).png) |

Os testes com modelos como ARIMA e Prophet resultaram em acurácias próximas de 50%. Isso levou a uma **mudança estratégica fundamental**: o problema foi reformulado de uma previsão de valor para uma **tarefa de classificação (Alta vs. Baixa)**, focada em Machine Learning.

| Falha dos Modelos de Série Temporal (Previsão de Preço) | Falha do Modelo Híbrido |
| :---: | :---: |
| *Modelos como Prophet e SARIMAX não conseguiram acompanhar os movimentos reais.* | *Mesmo um modelo híbrido (Prophet+XGBoost) não atingiu a performance desejada.* |
| ![Falha Previsão de Preço](img/download%20(43).png) | ![Modelo Híbrido](img/download%20(45).png) |

---

## 5. Fase Final: Engenharia de Features e Modelagem por Classificação

Esta fase consolidou a nova estratégia, focando em enriquecer o dataset com features robustas e aplicar uma metodologia de treinamento rigorosa.

#### 5.1. Engenharia e Seleção de Features
Foi criado um rico conjunto de mais de 30 features, incluindo lags, médias móveis, volatilidade e indicadores técnicos (RSI, MACD). A prevenção de *data leakage* foi garantida com o uso de `.shift(1)`. Uma análise de **Feature Importance** com XGBoost foi utilizada para ranquear e selecionar as variáveis mais preditivas.

#### 5.2. Metodologia de Validação e Otimização
Foi adotada uma abordagem robusta para garantir a confiabilidade do modelo:
- **Balanceamento de Classes (SMOTE):** Para evitar viés, a classe minoritária no conjunto de treino foi aumentada sinteticamente.
- **Divisão Treino-Validação-Teste:** Uma divisão cronológica rigorosa foi usada para otimizar os hiperparâmetros e realizar uma avaliação final imparcial.

| Balanceamento de Classes (SMOTE) | Divisão Treino/Validação/Teste |
| :---: | :---: |
| ![SMOTE](img/imbalanced.webp) | ![Divisão Treino/Validação/Teste](img/training-validation-test-data-set.png) |

#### 5.3. Resultados do Modelo Final Campeão (XGBoost)
Após um processo sistemático de seleção de features e otimização, o **XGBoost** se destacou, alcançando os seguintes resultados no conjunto de teste final:

| Métrica | Resultado |
| :--- | :--- |
| ✅ **Acurácia** | **80,00%** |
| 🎯 **AUC (Área Sob a Curva ROC)** | **0.73** |
| **Recall (Alta)** | 79% |
| **Recall (Baixa)** | 18% |

**Análise Visual da Performance:**

| Matriz de Confusão | Curva ROC |
| :---: | :---: |
| *A matriz mostra 24 acertos em 30 dias de teste.* | *A AUC de 0.73 indica um bom poder de discriminação do modelo.* |
| ![Matriz de Confusão](img/download%20(46).png) | ![Curva ROC](img/download%20(47).png) |

**Análise de Acertos e Erros na Janela de Teste:**
*Este gráfico visualiza a performance dia a dia, validando a alta acurácia do modelo.*
![Análise de Acertos e Erros](img/download%20(48).png)

---

## 6. Conclusão e Teoria do Projeto

Este projeto cumpriu o objetivo de desenvolver um modelo preditivo com performance superior à meta de 75%. A **teoria central validada** é que o sucesso na previsão de curto prazo do mercado financeiro reside em **traduzir a dinâmica temporal em um conjunto rico de features** e utilizar um algoritmo robusto como o **XGBoost** para aprender os padrões não-lineares.

O modelo final, com **80% de acurácia**, prova ser uma ferramenta quantitativa valiosa. Futuras iterações podem explorar a inclusão de dados exógenos (taxa de juros, câmbio, sentimento de notícias) para aprimorar ainda mais sua capacidade preditiva.

Para uma análise aprofundada da metodologia, dos resultados e das conclusões, consulte o relatório técnico completo disponível em formato PDF no repositório.
---

## 7. Como Replicar o Projeto

1.  Clone este repositório.
2.  Instale as dependências: `pip install pandas numpy scikit-learn xgboost lightgbm imbalanced-learn matplotlib seaborn jupyter`.
3.  Execute os notebooks Jupyter na ordem numérica (`01` a `04`).

---

## 8. Autor

**Joe Allan Zirn**
- [LinkedIn](https://www.linkedin.com/in/joe-allan-zirn-2bb0b62b1/)
