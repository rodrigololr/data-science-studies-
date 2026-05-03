# Lista 2 — Credit Card Fraud Detection
## Manual de Algoritmos e Metodologia

**Aluno:** Antônio Rodrigo Lima de Andrade Tenório
**Base:** creditcard.csv (Kaggle Credit Card Fraud Detection)
**Data:** 2026

---

## Visão Geral do Dataset

| Característica | Valor |
|----------------|-------|
| Total de transações | 284.807 |
| Features | Time, V1–V28 (PCA), Amount |
| Target | Class (0=legítimo, 1=fraude) |
| Proporção de fraudes | 0,172% (492 fraudes) |
| Valores ausentes | 0 |
| Duplicatas | 1.081 (já removidas na Lista 1) |

> **Nota:** As features V1–V28 são componentes principais anonimizados via PCA. Apenas `Time` e `Amount` mantêm formato original.

---

## Q1 — Definição do Problema Analítico

### Algoritmo: Análise Exploratória Sistemática

```
1. Carregar dataset
2. Analisar dimensionalidade (linhas × colunas)
3. Verificar tipos de dados
4. Quantificar missing values
5. Analisar distribuição do target (Class)
6. Calcular correlação entre features
7. Gerar resumo técnico automatizado
```

### Decisão Metodológica

Após análise, определянmos que o problema é **classificação binária probabilística**:

- **Target é binário** (0 ou 1) → regressão pura não é ideal
- **Precisamos de probabilidades** para decisão de fraude → classificação pura não aproveita incerteza
- **Dados altamente desbalanceados** (0,17% fraudes) → métricas devem ser sensíveis a classe minoritária

### Função de Resumo Técnico

```python
def resumo_base(df, target='Class'):
    # Retorna dicionário com:
    # - dimensionalidade
    # - tipos de dados
    # - distribuição do target
    # - correlação média entre features
    # - score de adequação ao método
```

### Conclusão Esperada

O problema é adequadamente tratado como **classificação binária com probabilidades**, onde:
- Métricas primárias: precision, recall, F1-score, ROC-AUC
- Métricas secundárias: matriz de confusão, curvas PR
- Validação: stratified split para manter proporções de classe

---

## Q2 — Naive Bayes

### Algoritmo: Teorema de Bayes com Independência Condicional

```
P(classe | features) ∝ P(features | classe) × P(classe)

Para features contínuas (GaussianNB):
P(x|c) = (1 / √(2πσ²)) × exp(-(x-μ)²/2σ²)

Para features discretizadas (BernoulliNB):
P(x|c) = p^c × (1-p)^(1-c)  (distribuição Bernoulli)
```

### Variações Implementadas

| Variante | Quando Usar | Pressuposto |
|----------|-------------|-------------|
| **GaussianNB** | Features contínuas (V1–V28, Amount) | Features seguem distribuição normal dado cada classe |
| **BernoulliNB** | Features binárias (discretização em bins) | Cada feature é binária (presente/ausente) |

### Impacto do Pré-processamento

```
SEM StandardScaler:
- Features com escalas diferentes (Amount: 0–25691, V1: -45 a 12)
- GaussianNB assume mesma variância → performance degradada

COM StandardScaler:
- Todas as features na mesma escala (μ=0, σ=1)
- GaussianNB Treats all features equally → melhor performance
```

### Discussão: Pressuposto de Independência

> **Problema Known:** As features V1–V28 são componentes PCA — logo, são ortogonais por construção!

Na prática:
- PCA garante que V1–V28 são **linearmente independentes**
- Mas Naive Bayes assume **independência condicional dado o target** — isso é diferente
- Correlações podem existir condicionalmente às classes (fraude vs legítimo)

### Métricas de Avaliação

```python
# Para base desbalanceada, ACCURACY É MENTIRA!
metrics = {
    'precision_score': 'Quando prevemos fraude, quantas são reais?',
    'recall_score': 'De todas as fraudes, quantas detectamos?',
    'f1_score': 'Média harmônica precision/recall',
    'roc_auc_score': 'Capacidade de ranking do modelo',
    'confusion_matrix': 'FP, FN, VP, VN'
}
```

### Conclusão Esperada

1. GaussianNB deve performar **melhor que BernoulliNB** (dados contínuos)
2. StandardScaler deve **melhorar** performance do GaussianNB
3. O pressuposto de independência é **razoável** para features PCA (já ortogonais)
4. Recall pode ser baixo se o modelo for muito conservador

---

## Q3 — Regressão

### Algoritmo: Regressão Linear Múltipla

```
Amount_predito = β₀ + β₁×Time + β₂×V1 + β₃×V2 + ... + β₃₁×Class + ε

Minimização: MSE = Σ(y_actual - y_predicted)² / n
Regularização Ridge: adiciona λΣβ² ao loss (shrinkage de coeficientes)
```

### Variações Implementadas

| Modelo | Objetivo | Regularização |
|--------|----------|---------------|
| **LinearRegression** | Baseline | Nenhuma |
| **Ridge Regression** | Prevenir overfitting | L2 (λΣβ²) |

### Por que regressão no Amount?

- Amount é **contínuo** (0 a 25.691)
- Fraudes podem ter **padrões de valor** específicos
- Podemos modelar Amount = f(features) para entender anomalias

### Análise de Resíduos

```
Resíduo = y_actual - y_predicted

1. HOMOCEDASTICIDADE:
   - Gráfico: resíduos vs valores preditos
   - Padrão em cone = heterocedasticidade (problema!)
   - Variância constante = bom

2. NÃO-LINEARIDADE:
   - Gráfico: resíduos vs features
   - Padrões não-aleatórios = relação não-linear capturada

3. OUTLIERS:
   - Resíduos studentizados > 3 = outlier influente
   - Verificar com DFFITS ou Cook's distance
```

### Métricas de Avaliação

```python
metrics_regression = {
    'MAE': 'Erro absoluto médio (na unidade original)',
    'MSE': 'Erro quadrático médio (penaliza grandes erros)',
    'RMSE': 'Raiz do MSE (interpretável na unidade original)',
    'R²': 'Proporção de variância explicada (0–1, maior = melhor)'
}
```

### Conclusão Esperada

1. R² provavelmente **baixo** (fraudes são raros, Amount não explica tudo)
2. Alguns features (V1–V28) devem ter coeficientes **não significativos**
3. Resíduos devem mostrar **heterocedasticidade** (Amount tem cauda longa)
4. Ridge deve produzir coeficientes mais **estáveis**

---

## Q4 — Árvore de Decisão

### Algoritmo: Decision Tree Classifier

```
ID3/CART - Construção recursiva:

1. Começa com todos os dados no nó raiz
2. Para cada feature f e cada ponto de corte t:
   - Calcula impureza (Gini ou Entropy)
   - Gini = 1 - Σp²
   - Entropy = -Σp × log₂(p)
3. Escolhe (f, t) que maximiza ganho de informação
4. Divisão recursiva até critério de parada

Ganho de Informação:
IG = Impureza(parent) - WeightedAvg(Impureza(children))
```

### Variações de Hiperparâmetros

| Parâmetro | Efecto | Valores Testados |
|-----------|--------|-------------------|
| **max_depth** | Limita profundidade máxima | 3, 5, 10, None |
| **criterion** | Métrica de divisão | 'gini', 'entropy' |
| **min_samples_split** | Mínimo amostras para dividir | 2, 10, 50 |
| **min_samples_leaf** | Mínimo amostras na folha | 1, 5, 10 |

### Feature Importance

```
Importância = Σ (Ganho × N_samples) / N_total
              para todas as divisões onde a feature foi usada

Features mais importantes = melhores preditoras de fraude
```

### Visualização

```python
plot_tree(decision_tree,
         feature_names=['Time', 'V1', 'V2', ..., 'V28', 'Amount'],
         class_names=['Legitimo', 'Fraude'],
         max_depth=4,  # profundidade limitada para legibilidade
         filled=True)  # cores por classe majoritária
```

### Interpretabilidade vs Desempenho

| Aspecto | Decision Tree | NB/Regressão |
|---------|--------------|--------------|
| Interpretabilidade | **Alta** (regras explícitas) | Média |
| Performance | Boa | Boa |
| Overfitting | Risco (profundidade alta) | Menor com regularização |
| Captura interações | Sim | Não sem engineering |

### Conclusão Esperada

1. Árvore deve identificar **regras de decisão** intuitivas
2. Features V1, V2, V3, V4, V14, V17 provavelmente **mais importantes** (padrão em literatura)
3. Profundidade 5–10 deve ser **ótimo trade-off**
4. Comparação com NB: se accuracy similar, tree é preferível por **interpretabilidade**

---

## Q5 — Comparação de Modelos

### Algoritmo: Validação Cruzada Estratificada

```
Para cada modelo (NB, DecisionTree, LogisticRegression):
    1. Dividir dados (stratified split 70/30)
    2. Treinar com train set
    3. Validar com test set
    4. Calcular métricas
    5. Repetir com cross_val_score (k=5)

Métricas registradas:
- accuracy, precision, recall, f1 (global e por classe)
- roc_auc_score
- tempo de treino
- tempo de predição
```

### Modelos Comparados

| Modelo | Tipo | Família |
|--------|------|---------|
| **GaussianNB** | Classificação probabilística | Bayesiana |
| **DecisionTreeClassifier** | Regra baseada em splitting | Ensemble base |
| **LogisticRegression** | Classificação linear | Estatístico |

### Análise de Robustez

```
ROBUSTEZ = estabilidade das métricas através de folds

- Se desvio padrão das métricas entre folds é BAIXO → modelo estável
- Se desvio padrão é ALTO → modelo sensível à divisão dos dados

Para base desbalanceada:
- Usar StratifiedKFold (mantém proporção de classes)
- Reportar métricas por classe (não apenas global)
```

### Critérios de Escolha

| Critério | Pergunta | Peso |
|----------|---------|------|
| Performance | Qual tem melhor F1/ROC-AUC? | Alto |
| Robustez | Qual é mais estável entre splits? | Alto |
| Custo Computacional | Qual treina mais rápido? | Médio |
| Interpretabilidade | Qual é mais explicável? | Médio |
|泛化能力 | Qual funciona melhor em novos dados? | Alto |

### Conclusão Esperada

1. **DecisionTree** deve ter melhor performance bruta
2. **GaussianNB** deve ser mais rápido mas talvez menos preciso
3. **LogisticRegression** pode ser competitivo com bom pré-processamento
4. Para produção: DecisionTree ou LogisticRegression (mais estáveis)

---

## Q6 — Séries Temporais

### Algoritmo: Agregação Temporal + Decomposição

```
PASSO 1: Agregação por intervalo de tempo
    df['Hour'] = (df['Time'] / 3600).astype(int)  # 1 hora
    serie = df.groupby('Hour').agg({
        'Amount': 'sum',
        'Class': ['count', 'sum']  # total transações, qtd fraudes
    })

PASSO 2: Visualização
    - Plot da série temporal
    - Decomposição (tendência + sazonalidade)

PASSO 3: Previsão
    - Naive: último valor
    - Média móvel (window=24)
```

### Decomposição de Séries

```
Serie(t) = Tendência(t) + Sazonalidade(t) + Resíduo(t)

- Tendência: média móvel suavizada (captura direção geral)
- Sazonalidade: padrão que se repete (diário, semanal)
- Resíduo: variação aleatória não explicada
```

### Limitações do Dataset

| Limitação | Impacto | Solução |
|-----------|---------|---------|
| Time é segundos desde início | Não temos timestamp real | Agregar por elapsed time |
| Sem data/hora calendar | Não há sazonalidade real | Usar Time relativo |
| Apenas ~48 horas de dados | Sazonalidade semanal invisível | Limitar claims |
| Muitas transações | Agregaçãonecessária | Resampling para 1 hora |

### Métricas de Avaliação

```python
from statsmodels.tsa.seasonal import seasonal_decompose

decomposition = seasonal_decompose(serie, model='additive', period=24)
# period=24 → padrão diário предполагается

# Avaliar:
# - Tendência: monotonic? crescente?
# - Sazonalidade: amplitude? padrão regular?
# - Resíduo: autocorrelação? (residuos não devem ter padrão)
```

### Conclusão Esperada

1. Série deve mostrar **picos de atividade** em ciertos horários
2. **Sazonalidade diária** pode existir (pessoas compram em horários específicos)
3. Tendência deve ser relativamente **estável** (dados de 2 dias)
4. Previsão por média móvel deve ser **baseline razoável**

---

## Q7 — Análise de Redes

### Algoritmo: Rede de Correlações entre Features

```
PASSO 1: Calcular matriz de correlação
    corr_matrix = df[['V1','V2',...,'V28']].corr()

PASSO 2: Construir grafo
    G = nx.Graph()
    for i, feature_i in enumerate(V_features):
        for j, feature_j in enumerate(V_features):
            if i < j and abs(corr_matrix.iloc[i,j]) > threshold:
                G.add_edge(feature_i, feature_j,
                           weight=abs(corr_matrix.iloc[i,j]))

PASSO 3: Calcular métricas
    degree = dict(G.degree())
    centrality = nx.betweenness_centrality(G)
    communities = nx.community.louvain(G)
```

### Interpretação das Métricas

| Métrica | Significado | Uso |
|---------|-------------|-----|
| **Degree** | Número de conexões por nó | Identificar features mais conectadas |
| **Betweenness Centrality** | Frequência em caminhos mais curtos | Features que conectam clusters |
| **Closeness Centrality** | Distância média para outros nós | Features "centrais" |
| **Communities** | Grupos de features similares | Identificar clusters de correlação |

### Threshold de Correlação

```
|weight| > 0.5 (50%) → aresta presente
|weight| < 0.5 → aresta removida (ruído)

Justificativa:
- 0.3-0.5: correlação moderada (pode ser ruído)
- 0.5-0.7: correlação forte (valor interpretativo)
- > 0.7: correlação muito forte (multicolinearidade)
```

### Visualização

```python
import networkx as nx
import matplotlib.pyplot as plt

pos = nx.spring_layout(G, k=2)  # layout force-directed
nx.draw(G, pos,
        node_color='lightblue',
        node_size=500,
        with_labels=True,
        font_size=8)
```

### Discussão: Valor Acrescentado

| Argumento | Avaliação |
|-----------|-----------|
| Identificar features correlacionadas | **Útil** para feature selection |
| Entender estrutura dos dados | **Limitado** (features são PCA) |
| Detectar anomalias em redes | **Fraco** (não é grafo natural) |

### Conclusão Esperada

1. Devem haver **clusters** de features correlacionadas
2. **V1-V28 são PCA** → correlações são artifact do PCA ou genuínas?
3. Análise é mais **metodológica** que prática para este dataset
4. Features mais centrais podem ser **mais importantes** para modelos

---

## Q8 — Meta-aprendizagem

### Algoritmo: Experimentos Sistemáticos

```
META: Entender QUANDO cada modelo funciona melhor

EXPERIMENTO 1: Subconjuntos de Features
    subsets = {
        'V1-V10': df[['V1',...,'V10']],
        'V11-V20': df[['V11',...,'V20']],
        'V21-V28': df[['V21',...,'V28']],
        'all': df[['V1',...,'V28']]
    }
    # Treinar NB, DT em cada subset → comparar F1

EXPERIMENTO 2: Pré-processamento
    configs = {
        'raw': X_train, X_test,
        'scaled': StandardScaler().fit_transform(X_train),
    }

EXPERIMENTO 3: Particionamento
    ratios = [(0.7,0.3), (0.8,0.2), (0.9,0.1)]

EXPERIMENTO 4: Balanceamento
    strategies = ['none', 'class_weight=balanced']
```

### Análise de Padrões

```python
# REGRA TÉCNICA: qual modelo escolher baseado nos dados
if dados_tem_muitas_features_correlacionadas:
    modelo = "DecisionTree"  # captura interações
elif dados_sao_alta_dimensionalidade:
    modelo = "NaiveBayes"      # treat each feature independently
elif dados_precisam_interpretabilidade:
    modelo = "DecisionTree"    # regras explícitas
elif dados_sao_muito_desbalanceados:
    modelo = "LogisticRegression"  # suporte a class_weight
```

### Framework de Recomendação

| Condição | Modelo Recomendado | Justificativa |
|----------|-------------------|---------------|
| Alta dimensionalidade + features independentes | GaussianNB | Trata cada feature independentemente |
| Features com interações complexas | DecisionTree | Captura não-linearidades |
| Necessidade de probabilidades | LogisticRegression | Saída calibrada |
| Muitas correlações entre features | Regularized Regression | Shrinkage de coeficientes |

### Conclusão Esperada

1. **DecisionTree** deveperformar melhor com todas as features
2. **GaussianNB** pode ser competitivo em subsets menores
3. **StandardScaler** deve ajudar NB e DT
4. **class_weight='balanced'** deve melhorar recall paraminoritária
5. Padrões identificados devem formar **regra de escolha** reproduzível

---

## Q9 — Visualização de Dados

### Algoritmo: Dashboard Analítico

```
PAINEL DE VISUALIZAÇÕES:

1. DISTRIBUIÇÃO DE AMOUNT
   - Histograma (log scale)
   - Boxplot por classe

2. HEATMAP DE CORRELAÇÕES
   - V1-V28 vs Class
   - Identificar features mais correlacionadas com fraude

3. PRECISION-RECALL CURVES
   - Comparar modelos (NB, DT, LR)
   - Curva ideal: canto superior direito

4. FEATURE IMPORTANCE
   - DecisionTree vs NaiveBayes
   - Comparar ranking de importância

5. SÉRIE TEMPORAL
   - Transações por hora
   - Fraudes por hora

6. CONFUSION MATRICES
   - Grid de 2x2 para cada modelo
```

### Princípios de Visualização

| Princípio | Aplicação |
|-----------|-----------|
| **Minimalismo** | Removerchartjunk, focar no dado |
| **Cores significativas** | Vermelho=fraude, verde=legítimo |
| **Proporção áurea** | Aspect ratio 1:1.618 |
| **Contexto** | Eixos rotulados, legends claras |

### Ferramentas

```python
import matplotlib.pyplot as plt
import seaborn as sns

sns.set_theme(style="whitegrid")
plt.rcParams["figure.figsize"] = (12, 8)
```

### Justificativa das Visualizações

| Visualização | Decisão Metodológica Defendida |
|--------------|-------------------------------|
| Histogramade Amount | Mostra cauda longa → outlier treatment |
| Heatmap correlação | Identifica features importantes para feature selection |
| PR Curves | Mais honestas que ROC para base desbalanceada |
| Feature Importance | Justifica escolha de variáveis para modelo |

### Conclusão Esperada

1. Dashboard deve comunicar **resultados-chave** em 1 página
2. Visualizações devem **defender decisões** (não apenas descrever)
3. Gráficos comparativos (modelos) devem mostrar **superioridade de um**
4. Time series deve mostrar **padrões temporais** de fraude

---

## Q10 — Consolidação da Solução

### Algoritmo: Pipeline Organizado + Relatório Automático

```
COMPONENTES DO RELATÓRIO:

1. FUNÇÕES REUTILIZÁVEIS
   - resumo_base()        # Q1
   - treinar_naive_bayes() # Q2
   - treinar_regressao()   # Q3
   - treinar_arvore()      # Q4
   - comparar_modelos()    # Q5
   - serie_temporal()      # Q6
   - rede_visualizacao()   # Q7
   - meta_analise()        # Q8
   - dashboard_final()     # Q9

2. TABELA COMPARATIVA
   | Modelo | F1 | ROC-AUC | Tempo |
   |--------|----|---------|-------|
   | NB     | .  |    .    |   .   |
   | DT     | .  |    .    |   .   |
   | LR     | .  |    .    |   .   |

3. LIMITAÇÕES DO DATASET
   - Features anonimizadas (V1-V28) limitam interpretabilidade
   - Time é relativo (não timestamp real)
   - Base desbalanceada (0.17% fraudes)
   - Apenas 2 dias de dados

4. RECOMENDAÇÃO EXECUTIVA
   - Qual modelo escolher para produção?
   - Qual threshold de probabilidade usar?
   - Quais ações baseadas no modelo?
```

### Relatório Automático

```python
def gerar_relatorio_final(modelos, metricas, limitacoes):
    """
    Gera relatório Markdown com:
    1. Resumo executivo
    2. Tabela comparativa
    3. Visualizações principais
    4. Limitações
    5. Recomendação
    """
    print("# RELATÓRIO FINAL")
    print("## Comparação de Modelos")
    print(metricas.to_string())
    print("## Recomendação")
    print(recomendacao)
```

### Critério de Recomendação Final

| Modelo | Vantagem Principal | Desvantagem | Uso Indicado |
|--------|-------------------|-------------|-------------|
| **GaussianNB** | Rápido, probabilístico | Pressupostos fortes | Baseline, primeiros drafts |
| **DecisionTree** | Interpretabilidade | Overfitting risk | Quando explicabilidade importa |
| **LogisticRegression** | Estável, calibrado | Linearidade | Produção, quando linear é suficiente |

### Conclusão Esperada

1. **DecisionTree** ou **LogisticRegression** deve ser recomendação final
2. Threshold de probabilidade deve ser ajustado para **balancear FP/FN**
3. Pipeline completo deve ser **reprodutível** com novos dados
4. Principais limitações: anonimização de features, desbalanceamento

---

## Resumo Metodológico

| Questão | Método Principal | Métrica Chave |
|---------|------------------|---------------|
| Q1 | Análise Exploratória | Adequação ao problema |
| Q2 | GaussianNB + BernoulliNB | F1, ROC-AUC |
| Q3 | LinearRegression + Ridge | R², RMSE |
| Q4 | DecisionTreeClassifier | F1, Feature Importance |
| Q5 | Cross-Validation | F1, ROC-AUC, Estabilidade |
| Q6 | Agregação Temporal | Tendência, Sazonalidade |
| Q7 | Grafo de Correlações | Centralidade, Communities |
| Q8 | Experimentos Sistemáticos | Padrões de performance |
| Q9 | Dashboard Visual | Comunicação de resultados |
| Q10 | Pipeline Consolidação | Relatório automático |

---

## Referências

- Scikit-learn Documentation: https://scikit-learn.org/
- Seaborn Gallery: https://seaborn.pydata.org/
- NetworkX Documentation: https://networkx.org/
- Statsmodels Time Series: https://www.statsmodels.org/

---

*Documento gerado para estudos — Lista 2 de Ciência de Dados*
