````markdown
# 🚀 Modelo Preditivo para a Tendência do IBOVESPA

![Status: Concluído](https://img.shields.io/badge/Status-Concluído-brightgreen)
![Linguagem](https://img.shields.io/badge/Linguagem-Python_3-blue)
![Bibliotecas](https://img.shields.io/badge/Bibliotecas-Scikit--learn_|_XGBoost_|_Pandas-lightgrey)

### Tabela de Conteúdos
1. [Visão Geral do Projeto](#-visão-geral-do-projeto)
2. [Principais Destaques](#-principais-destaques)
3. [Metodologia do Projeto](#-metodologia-do-projeto)
4. [Tecnologias Utilizadas](#-tecnologias-utilizadas)
5. [Estrutura do Repositório](#-estrutura-do-repositório)
6. [Como Executar o Projeto](#-como-executar-o-projeto)
7. [Resultados do Modelo Final](#-resultados-do-modelo-final)
8. [Conclusão](#-conclusão)
9. [Autor](#-autor)

## 📝 Visão Geral do Projeto

Este projeto apresenta o desenvolvimento de um modelo de Machine Learning para prever a tendência de fechamento (**alta** ou **baixa**) do índice IBOVESPA no dia seguinte. Utilizando um extenso histórico de dados diários, o modelo foi construído para servir como um insumo em dashboards, auxiliando analistas quantitativos na tomada de decisão.

O trabalho aborda o ciclo completo de um projeto de Data Science, desde a limpeza e análise exploratória dos dados até a engenharia de features, otimização de modelos e validação robusta dos resultados.

## ✨ Principais Destaques

- **Performance Superior à Meta:** O modelo final alcançou **80% de acurácia** em um conjunto de teste não visto, superando a meta de 75% do desafio.
- **Metodologia Robusta:** Utilização de técnicas avançadas como Validação Cruzada para Séries Temporais (`TimeSeriesSplit`) e uma divisão `Treino-Validação-Teste` para garantir a generalização do modelo e evitar overfitting.
- **Análise Exploratória Profunda:** Geração de insights valiosos sobre os diferentes "regimes" do mercado, a natureza não-estacionária da série e o fenômeno das "caudas gordas" nos retornos diários.
- **Engenharia de Features:** Criação de um rico conjunto de features (lags, médias móveis, volatilidade, indicadores técnicos como RSI e MACD) e uma metodologia sistemática para selecionar as mais preditivas.
- **Justificativa Estratégica:** O relatório documenta a transição de modelos de série temporal clássicos (ARIMA, Prophet), que se mostraram inadequados, para uma abordagem de classificação supervisionada, que se provou muito mais eficaz.

## 📊 Metodologia do Projeto

O projeto seguiu um fluxo de trabalho estruturado para garantir a qualidade e a confiabilidade dos resultados:

**1. Limpeza e Preparação** → **2. Análise Exploratória (EDA)** → **3. Modelagem Inicial (Série Temporal)** → **4. Pivô Estratégico** → **5. Engenharia de Features Avançada** → **6. Otimização e Validação** → **7. Modelo Final (XGBoost)**

## 🛠️ Tecnologias Utilizadas

- **Linguagem:** Python 3
- **Bibliotecas Principais:**
  - `Pandas` e `NumPy` para manipulação de dados.
  - `Scikit-learn` para pré-processamento, métricas e modelagem.
  - `XGBoost` e `LightGBM` para os modelos de Gradient Boosting.
  - `imbalanced-learn` para balanceamento de classes (SMOTE).
  - `Matplotlib` e `Seaborn` para visualização de dados.
- **Ambiente:** Jupyter Notebook

## 📁 Estrutura do Repositório

O projeto está organizado em notebooks sequenciais que contam a história do desenvolvimento:

- **`01_exploracao_e_limpeza.ipynb`**: Carregamento, limpeza e padronização dos dados brutos do IBOVESPA.
- **`02.Análise_exploratória_dos_dados.ipynb`**: Análise visual e estatística para extrair insights sobre a série histórica.
- **`03_SérieTemporal.ipynb`**: Primeiras tentativas de modelagem com abordagens de série temporal (Decomposição, ARIMA, Prophet) e a justificativa para a mudança de estratégia.
- **`04_Featured_enginerring_e_treinamento_modelos.ipynb`**: O notebook principal, contendo a engenharia de features, o benchmark de modelos, a seleção de features, a otimização de hiperparâmetros e a avaliação do modelo final.

## ⚙️ Como Executar o Projeto

Siga os passos abaixo para replicar os resultados.

### Pré-requisitos
- Python 3.8 ou superior
- Git

### Setup
1. Clone este repositório:
   ```bash
   git clone [https://github.com/seu-usuario/nome-do-repositorio.git](https://github.com/seu-usuario/nome-do-repositorio.git)
````

2.  Navegue até a pasta do projeto:
    ```bash
    cd nome-do-repositorio
    ```
3.  Instale as dependências (recomenda-se o uso de um ambiente virtual):
    ```bash
    pip install -r requirements.txt
    ```

### Execução

Abra os notebooks Jupyter na ordem numérica (`01` a `04`) e execute as células para reproduzir cada etapa da análise e modelagem.

## 📈 Resultados do Modelo Final

O modelo campeão foi um **XGBoost** treinado com 5 features selecionadas e hiperparâmetros otimizados. Sua performance no conjunto de teste final (30 dias não vistos) foi:

| Métrica | Resultado |
| :--- | :--- |
| **Acurácia** | **80,00%** |
| **AUC (Área Sob a Curva ROC)** | **0.81** |
| **Precision (Classe Alta)** | 0.88 |
| **Recall (Classe Alta)** | 0.78 |
| **Precision (Classe Baixa)** | 0.71 |
| **Recall (Classe Baixa)** | 0.83 |

### Visualização da Performance

**Matriz de Confusão**
*(Esta matriz detalha os acertos e erros do modelo, mostrando seu bom desempenho em ambas as classes)*

**Curva ROC**
*(A AUC de 0.81 demonstra o excelente poder de discriminação do modelo entre dias de alta e baixa)*

**Importância das Features**
*(O modelo baseou suas decisões principalmente em sinais de reversão à média e anomalias de volume)*

## 🧠 Conclusão

O projeto cumpriu com sucesso o objetivo de criar um modelo preditivo com performance superior a 75%. A principal teoria validada foi a de que, para prever a direção diária do IBOVESPA, uma abordagem de **classificação com engenharia de features robusta** é mais eficaz do que modelos de série temporal clássicos.

O modelo final **XGBoost**, com **80% de acurácia**, prova ser uma ferramenta quantitativa valiosa para complementar a análise e a tomada de decisão no mercado de capitais. Como próximos passos, sugere-se a inclusão de dados exógenos (taxa de juros, câmbio, sentimento de notícias) para aprimorar ainda mais a capacidade preditiva do modelo.

## 📬 Autor

**Ana Raquel**

  - [LinkedIn](https://www.google.com/search?q=https://www.linkedin.com/in/seu-linkedin/)
  - [GitHub](https://www.google.com/search?q=https://github.com/seu-usuario)

<!-- end list -->

```
```
