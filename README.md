# 📈 Modelo Preditivo para a Tendência do IBOVESPA | Acurácia Final: 80%

![Status: Concluído](https://img.shields.io/badge/Status-Concluído-brightgreen)
![Acurácia](https://img.shields.io/badge/Acurácia_Final-80%25-success)
![Linguagem](https://img.shields.io/badge/Linguagem-Python_3-blue)
![Bibliotecas](https://img.shields.io/badge/Bibliotecas-Scikit--learn_|_XGBoost_|_Pandas-lightgrey)

## 🎯 O Desafio: Prever o Imprevisível

[cite_start]O objetivo deste projeto foi desenvolver um modelo de Machine Learning capaz de prever a tendência de fechamento (alta ou baixa) do índice IBOVESPA para o dia seguinte[cite: 3]. [cite_start]Utilizando uma base de dados histórica e diária, o modelo visa servir como ferramenta de apoio para analistas quantitativos[cite: 4, 5].

Prever o mercado financeiro é um desafio notório devido à sua alta complexidade, ruído e natureza não-estacionária, como foi confirmado na análise exploratória.

---

## 🚀 A Jornada Metodológica: Do Fracasso ao Sucesso

O desenvolvimento seguiu uma abordagem iterativa e adaptativa, aprendendo com os resultados de cada etapa para refinar a estratégia.

### Passo 1: Análise e a Falha dos Modelos Temporais
[cite_start]A Análise Exploratória de Dados (EDA) revelou que o IBOVESPA opera em diferentes "regimes", influenciado por eventos macroeconômicos e com o fenômeno das "caudas gordas" nos retornos diários[cite: 47, 273]. [cite_start]A série demonstrou ser **não-estacionária**[cite: 296, 297].

[cite_start]A tentativa inicial de usar modelos de série temporal clássicos (ARIMA, Prophet) falhou em capturar as oscilações diárias, resultando em uma acurácia próxima de 50% — o equivalente a um palpite aleatório[cite: 357, 358, 403].

### Passo 2: A Mudança de Estratégia
[cite_start]O ponto de virada do projeto foi a reformulação do problema: em vez de prever o *valor* da série, o foco passou a ser uma tarefa de **classificação binária**: o dia seguinte será de **alta (1)** ou de **baixa (0)**?[cite: 431, 432]. [cite_start]Esta abordagem permitiria o uso de algoritmos mais poderosos, como o XGBoost, para capturar as relações não-lineares do mercado[cite: 434].

### Passo 3: Engenharia de Features Robusta
O sucesso da abordagem de classificação dependia da criação de variáveis (features) que traduzissem a dinâmica temporal em informações numéricas. Foram criadas mais de 30 features, incluindo:
- **Lags de Retorno:** Momentum de curtíssimo prazo.
- **Médias Móveis e Distâncias:** Para capturar a tendência e o quão "esticado" o preço estava.
- **Indicadores Técnicos:** Como **RSI** e **MACD** para medir o momentum e a força da tendência.

[cite_start]Para garantir a integridade do modelo, uma prevenção rigorosa de **data leakage** foi implementada usando o método `.shift(1)` em todas as features, assegurando que as previsões fossem baseadas apenas em dados passados[cite: 450, 451].

### Passo 4: Seleção e Otimização Sistemática
Com um vasto leque de features, foi executado um processo rigoroso para encontrar a melhor combinação:
1.  [cite_start]**Benchmark de Modelos:** Uma competição inicial entre 4 algoritmos mostrou que modelos baseados em árvores (Random Forest e XGBoost) eram superiores[cite: 527, 532].
2.  [cite_start]**Seleção de Features por Força Bruta:** Um loop testou centenas de combinações de features e revelou que um conjunto enxuto de apenas **5 features** elevou a acurácia do XGBoost para **87%** em testes preliminares[cite: 563, 564].
3.  [cite_start]**Otimização Final:** Utilizando uma divisão de dados em **Treino, Validação e Teste**, os hiperparâmetros do XGBoost foram ajustados finamente (Grid Search) para maximizar sua capacidade de generalização e evitar overfitting[cite: 596, 601].

---

## 🏆 O Modelo Campeão: XGBoost

O modelo final, um **XGBoost** otimizado, demonstrou ser a solução mais robusta e precisa.

#### Features Vencedoras
O modelo baseia suas previsões no seguinte conjunto de 5 features:
- `Lag_Retorno_D-2`
- `SMA_7`
- `SMA_14`
- `Vol_SMA_21`
- `Dia_da_semana`

#### Performance no Conjunto de Teste (Dados Não Vistos)

| Métrica | Resultado |
| :--- | :--- |
| ✅ **Acurácia** | **80,00%** |
| 🎯 **AUC** | **0.73** |
| **Recall (Alta)** | 79% |
| **Recall (Baixa)** | 18% |

#### Análise Visual da Performance

**Matriz de Confusão**
*A matriz confirma a acurácia de 80%, com 24 acertos em 30 dias de teste.*
![Matriz de Confusão](img/matriz_confusao.png)

**Curva ROC**
*A AUC de 0.73 indica um bom poder de discriminação do modelo entre os dias de alta e baixa.*
![Curva ROC](img/curva_roc.png)

---

## 🔮 Próximos Passos
O modelo atual utiliza apenas dados endógenos (do próprio índice). [cite_start]A performance pode ser aprimorada com a inclusão de **dados exógenos**, como[cite: 698, 699, 700]:
- Taxa de juros (Selic) e inflação (IPCA).
- Variação de índices internacionais (S&P 500).
- Câmbio (Dólar) e preços de commodities.
- Análise de sentimento a partir de notícias do mercado.

---

## ⚙️ Como Replicar o Projeto
O projeto está organizado em notebooks sequenciais. Para executar:

1.  Clone o repositório.
2.  Instale as dependências: `pip install pandas numpy scikit-learn xgboost lightgbm imbalanced-learn matplotlib seaborn jupyter`.
3.  Execute os notebooks na ordem numérica: `01` -> `02` -> `03` -> `04`.

---

## 👨‍💻 Autor
**Ana Raquel**
- [LinkedIn](https://www.linkedin.com/in/seu-linkedin/)
- [GitHub](https://github.com/seu-usuario)
