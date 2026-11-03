# Data Science Studies & Applied Machine Learning Portfolio

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue.svg)](https://www.python.org/)
[![Scikit-Learn](https://img.shields.io/badge/scikit--learn-1.2%2B-F7931E.svg)](https://scikit-learn.org/)
[![Statsmodels](https://img.shields.io/badge/Statsmodels-0.13%2B-darkblue.svg)](https://www.statsmodels.org/)
[![NetworkX](https://img.shields.io/badge/NetworkX-3.0%2B-blue.svg)](https://networkx.org/)
[![Pandas](https://img.shields.io/badge/Pandas-1.5%2B-150458.svg)](https://pandas.pydata.org/)
[![NumPy](https://img.shields.io/badge/NumPy-1.22%2B-013243.svg)](https://numpy.org/)
[![SciPy](https://img.shields.io/badge/SciPy-1.9%2B-8CAAE6.svg)](https://scipy.org/)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebooks-orange.svg)](https://jupyter.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

Repositorio de **Ciencia de Dados, Aprendizado de Maquina Estatistico e Analise Multidisciplinar**. 

Reune investigacoes empiricas aprofundadas em cenarios de alta complexidade: deteccao de fraudes em dados massivos desbalanceados, decomposicao estocastica de series temporais, topologia de redes complexas, modelagem preditiva supervisionada e mineracao de microdados de seguranca publica de Alagoas.

---

## Sumario Executivo dos Projetos

| Projeto / Modulo | Dominio & Base | Foco Tecnico | Metodos & Algoritmos Chave | Principais Entregaveis |
|---|---|---|---|---|
| [**Lista 1: Deteccao de Fraude & Auditoria de Pipeline**](#1-lista-1---deteccao-de-fraude-financeira--auditoria-de-pipeline) | Financeiro / `creditcard.csv` (284k transacoes, 0.172% fraudes) | Diagnostico de Qualidade, Prevencao de Data Leakage e Modelagem k-NN | Auditoria IQR, Log-transform, `ColumnTransformer`, `RobustScaler`, `GridSearchCV`, k-NN, Regressao Logistica, Random Forest | Relatorio de auditoria tecnica ([`revisao_notebook.md`](./lista_1/revisao_notebook.md)) e notebook corrigido de ponta a ponta ([`Lista_1_Antonio_Rodrigo_melhorado.ipynb`](./lista_1/Lista_1_Antonio_Rodrigo_melhorado.ipynb)) |
| [**Lista 2: Manual Avancado de Algoritmos & Visual Analytics**](#2-lista-2---manual-avancado-de-algoritmos--visual-analytics) | Financeiro / `creditcard.csv` | Estudo Multiparadigma de 10 Dimensoes Analiticas | Naive Bayes (Gaussian/Bernoulli), Regressao Ridge, Arvores CART, Series Temporais (Statsmodels), Grafos e Redes (NetworkX) | Manual metodologico de 685 linhas ([`lista_2/README.md`](./lista_2/README.md)), notebook executado e 10 paineis graficos em alta resolucao |
| [**Projeto Final: Microdados de Seguranca Publica**](#3-projeto-final---analise-de-microdados-de-seguranca-publica-cvli-alagoas) | Seguranca Publica / `cvli-microdados-alagoas-2012-a-abril-de-2026.csv` | Analise Epidemiologica Criminal e Inteligencia Territorial | 14 atributos oficiais (2012-2026), sazonalidade temporal, manchas criminais por bairro/municipio, perfil demografico | Base consolidada, especificacao metodologica ([`descricao_projeto.md`](./projeto_cd/descricao_projeto.md)) e diretrizes de pitch executivo |
| [**Sintese Teorica & Avaliacao AB2**](#4-modulo-de-avaliacao-teorica-ab2--quiz-interativo) | Conceitual / Academico | Consolidacao Conceitual de Modelos Estatisticos e ML | Teorema de Bayes, OLS, Diagnostico de Residuos, CART/ID3, Medidas de Informacao, Validacao Estratificada | Banco de questoes resolvidas ([`ab2/questos_ab2_estudar.md`](./ab2/questos_ab2_estudar.md)) e aplicacao web interativa ([`quiz.html`](./quiz.html)) |

---

## Detalhamento dos Modulos

### 1. Lista 1 - Deteccao de Fraude Financeira & Auditoria de Pipeline
Diretorio: [`lista_1/`](./lista_1/) | Documentacao: [`lista_1/README.md`](./lista_1/README.md)

Estudo focado na deteccao de fraudes em cartao de credito sob o desafio de desbalanceamento extremo (apenas 492 fraudes em 284.807 transacoes - **0.172%**).

- **Auditoria de Qualidade e Inconsistencias:** Mapeamento de assimetria severa e presenca de mais de 18.000 outliers na variavel de montante (`Amount`), tratada por transformacoes logaritmicas e escalonamento robusto (`RobustScaler`).
- **Prevencao Rigorosa de Vazamento de Dados (*Data Leakage*):** O documento [`revisao_notebook.md`](./lista_1/revisao_notebook.md) registra a auditoria tecnica que corrigiu falhas estruturais de rascunhos anteriores, garantindo que transformadores estatisticos sejam ajustados (`fit`) estritamente nos dados de treino.
- **Otimizacao e Validacao:** Ajuste de hiperparametros via `GridSearchCV` para o classificador k-NN e comparacao multimodelo com foco em curvas Precision-Recall (PR-AUC) e F1-Score.
- **Arquivo de Referencia:** Utilize o notebook [`Lista_1_Antonio_Rodrigo_melhorado.ipynb`](./lista_1/Lista_1_Antonio_Rodrigo_melhorado.ipynb) para avaliacao tecnica.

---

### 2. Lista 2 - Manual Avancado de Algoritmos & Visual Analytics
Diretorio: [`lista_2/`](./lista_2/) | Manual Completo: [`lista_2/README.md`](./lista_2/README.md)

Uma das analises tecnicas mais extensas do repositorio, cobrindo 10 questoes que exploram diferentes familias matematicas de modelagem e visualizacao:

```
[ Base creditcard.csv ]
           |
  +--------+--------+-----------------+-----------------+
  |                 |                 |                 |
  v                 v                 v                 v
[ Q2: Naive Bayes ] [ Q3: Regressao ] [ Q4: Decision ]  [ Q6: Series ]
- GaussianNB        - OLS / Ridge     - CART / ID3      - Statsmodels
- BernoulliNB       - Residuos        - Gini/Entropia   - Decomposicao
- Independencia     - Heterocedast.   - Importancias    - Tendencia/Sazon.
           |                 |                 |                 |
           +--------+--------+-----------------+-----------------+
                    |
                    v
          [ Q7: Redes Complexas ] ----> Grafo de Correlacoes com NetworkX
                    |                   (Betweenness Centrality & Louvain)
                    v
          [ Q8: Meta-Aprendizagem ] --> Adequacao de modelos a dados
                    v
          [ Q9: Visual Analytics ] ---> Dashboard Integrado de Decisao
                    v
          [ Q10: Consolidacao ] ------> Pipeline de Inferencia Reproduzivel
```

#### Destaques Metodologicos da Lista 2:
- **Q1 - Formulacao Analitica:** Demonstracao de que o problema exige classificacao binaria probabilistica em vez de regressao direta ou classificacao rigida sem calibracao de probabilidades.
- **Q2 - Classificadores Bayesianos:** Comparacao entre `GaussianNB` e `BernoulliNB`. Avaliacao do pressuposto de independencia condicional dado o target versus a ortogonalidade das componentes PCA.
- **Q3 - Modelagem de Regressao e Diagnostico:** Regressao Linear e Ridge com penalizacao $L_2$ modelando o valor da transacao. Analise grafica de residuos demonstrando heterocedasticidade severa.
- **Q4 - Arvores de Decisao:** Inducao de arvores CART avaliando criterios de Gini e Entropia com variacao de profundidade maxima (`max_depth`) e identificacao das variaveis mais discriminantes ($V_{14}, V_{17}, V_4, V_2$).
- **Q5 - Robustez e Validacao Cruzada:** Avaliacao da estabilidade de metricas atraves de `StratifiedKFold` (desvios padrao entre dobras).
- **Q6 - Analise de Series Temporais:** Agregacao horaria dos dados de transacao e decomposicao aditiva (tendencia, sazonalidade e componente residual) com `statsmodels.tsa.seasonal.seasonal_decompose`.
- **Q7 - Teoria dos Grafos & Redes Complexas:** Construcao de grafo ponderado de correlacoes com `networkx`, calculando grau (*degree*), centralidade de intermediacao (*betweenness centrality*) e agrupamento em comunidades modulares.
- **Q8 - Meta-Aprendizagem:** Framework experimental sistematico mapeando qual familia de modelos performa melhor em funcao da dimensionalidade, correlacao e balanceamento de classes.
- **Q9 & Q10 - Visualizacao e Consolidacao:** Dashboard visual completo consolidado nos arquivos de imagem em `lista_2/` (`dashboard_final.png`, `visualizacao_curvas.png`, `visualizacao_importance.png`, `heatmap_correlacoes.png`, `visualizacao_confusion.png`).

---

### 3. Projeto Final - Analise de Microdados de Seguranca Publica (CVLI Alagoas)
Diretorio: [`projeto_cd/`](./projeto_cd/) | Documentacao: [`projeto_cd/README.md`](./projeto_cd/README.md)

Analise exploratoria e mineracao de dados orientada a tomada de decisao em politicas publicas a partir do conjunto oficial de dados de **Crimes Violentos Letais Intencionais (CVLI) em Alagoas de 2012 a abril de 2026**:
- **Dataset:** 14 campos detalhados incluindo data, hora, municipio, bairro, caracterizacao demografica da vitima (idade, sexo, raca/cor), instrumento do delito e tipologia do local.
- **Escopo Analitico:** Identificacao de pontos focais de recorrencia criminal, sazonalidade temporal (horarios e dias criticos), desproporcionalidade de vitimizacao e suporte a alocacao estrategica de policiamento ostensivo.
- **Formato Executivo:** Estruturacao orientada a apresentacao de *Pitch* defendendo recomendacoes fundamentadas em dados para gestores e banca avaliadora.

---

### 4. Modulo de Avaliacao Teorica (AB2) & Quiz Interativo
Diretorios: [`ab2/`](./ab2/) | [`quiz.html`](./quiz.html)

- **Sintese de Questoes ([`ab2/questos_ab2_estudar.md`](./ab2/questos_ab2_estudar.md)):** Revisao detalhada de questoes conceituais que consolidam topicos de aprendizado estatistico, analise de residuos, metricas de avaliacao, modelos lineares e particionamento de espacos.
- **Aplicacao Interativa ([`quiz.html`](./quiz.html)):** Interface web responsiva para simulacao de exames com correcao dinamica e temporizador para avaliacao do dominio em Ciencia de Dados.

---

## Estrutura do Repositorio

```
data-science-studies-/
├── README.md                           # Documentacao principal do portfolio
├── requirements.txt                    # Dependencias cientificas reproduziveis
├── quiz.html                           # Aplicacao web interativa de simulacao
│
├── lista_1/                            # MODULO 1: Deteccao de Fraude e Auditoria
│   ├── README.md                       # Documentacao e guia da Lista 1
│   ├── Lista_1_Antonio_Rodrigo_melhorado.ipynb # Notebook principal auditado e corrigido
│   ├── Lista_1_Antonio_Rodrigo_melhorado_rodado.ipynb # Versao executada com graficos
│   ├── revisao_notebook.md             # Auditoria tecnica de vazamento de dados
│   ├── Lista_1_Antônio_Rodrigo_completa.ipynb # Historico
│   └── lista_1_antônio_rodrigo*.py     # Scripts de suporte
│
├── lista_2/                            # MODULO 2: Analise Multiparadigma & Manual
│   ├── README.md                       # Manual de algoritmos e metodologia (685 linhas)
│   ├── Lista_2_Antonio_Rodrigo.ipynb   # Notebook completo com as 10 questoes resolvidas
│   ├── dashboard_final.png             # Painel visual consolidado
│   ├── visualizacao_curvas.png         # Curvas Precision-Recall comparativas
│   ├── visualizacao_importance.png     # Ranking de importancia de atributos
│   ├── visualizacao_confusion.png      # Matrizes de confusao multimodelo
│   ├── visualizacao_correlacao.png     # Heatmap de correlacoes
│   ├── serie_temporal.png              # Serie temporal de transacoes
│   ├── decomposicao_serie.png          # Tendencia, sazonalidade e residuo
│   └── questos_ab2_estudar.md          # Questoes conceituais complementares
│
├── projeto_cd/                         # PROJETO APLICADO: Seguranca Publica (CVLI)
│   ├── README.md                       # Dicionario de dados e objetivos analiticos
│   ├── cvli-microdados-alagoas-2012-a-abril-de-2026.csv # Microdados oficiais
│   ├── descricao_projeto.md            # Especificacao do projeto e formato pitch
│   └── Projeto (2026-1).pdf            # Diretrizes institucionais do IC/UFAL
│
└── ab2/                                # MODULO TEORICO: Questoes e Provas Anteriores
    ├── README.md                       # Guia de estudos para a avaliacao AB2
    ├── questos_ab2_estudar.md          # Sintese teorica de questoes resolvidas
    └── *.pdf                           # Provas historicas de Ciencia de Dados (UFAL)
```

---

## Tecnologias e Bibliotecas Utilizadas

- **Linguagem:** Python 3.10+
- **Manipulacao e Computacao Cientifica:** Pandas, NumPy, SciPy
- **Aprendizado de Maquina & Modelagem:** Scikit-Learn
- **Estatistica & Series Temporais:** Statsmodels
- **Analise de Redes Complexas:** NetworkX
- **Visualizacao de Dados:** Matplotlib, Seaborn
- **Computacao Interativa:** Jupyter Notebook, JupyterLab

---

## Como Executar o Projeto Localmente

### 1. Clonar o Repositorio
```bash
git clone https://github.com/rodrigololr/data-science-studies-.git
cd data-science-studies-
```

### 2. Configurar o Ambiente Virtual
```bash
# Linux / macOS:
python3 -m venv venv
source venv/bin/activate

# Windows:
python -m venv venv
venv\Scripts\activate
```

### 3. Instalar as Dependencias
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Iniciar o Jupyter
```bash
jupyter lab
# ou
jupyter notebook
```

Abra os notebooks em [`lista_1/Lista_1_Antonio_Rodrigo_melhorado.ipynb`](./lista_1/Lista_1_Antonio_Rodrigo_melhorado.ipynb) ou [`lista_2/Lista_2_Antonio_Rodrigo.ipynb`](./lista_2/Lista_2_Antonio_Rodrigo.ipynb) para reproduzir as analises.

---

## Autor

**Antônio Rodrigo Lima de Andrade Tenório**  
Instituto de Computacao (IC) - Universidade Federal de Alagoas (UFAL)  
- GitHub: [@rodrigololr](https://github.com/rodrigololr)
