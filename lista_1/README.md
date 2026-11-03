# Lista 1 - Deteccao de Fraude em Cartao de Credito

Projeto de deteccao de transacoes fraudulentas em dados massivos altamente desbalanceados utilizando a base `creditcard.csv` (284.807 transacoes com 492 fraudes - 0.172% de prevalencia).

---

## Estrutura dos Arquivos

| Arquivo | Descricao | Status |
|---|---|---|
| **`Lista_1_Antonio_Rodrigo_melhorado.ipynb`** | **Versao principal, corrigida e refatorada.** Pipeline sem vazamento de dados (*leakage-free*), espacos de atributos alinhados entre treino e teste e metricas corretas. | **Recomendado para avaliacao** |
| `Lista_1_Antonio_Rodrigo_melhorado_rodado.ipynb` | Versao executada com todos os outputs, graficos e tabelas geradas salvas nas celulas. | Versao compilada |
| `revisao_notebook.md` | Relatorio tecnico de auditoria que identificou potenciais fontes de vazamento de dados (*data leakage*) e desalinhamento de espaco de features em rascunhos anteriores. | Documento de auditoria |
| `Lista_1_Antônio_Rodrigo_completa.ipynb` | Versao anterior submetida a auditoria tecnica. | Arquivo historico |
| `Lista_1_Antônio_Rodrigo.ipynb` | Primeira versao inicial da lista. | Arquivo historico |

---

## Metodologia Aplicada na Versao Melhorada

A solucao cobre 10 questoes sequenciais estruturadas:

1. **Diagnostico Estrutural:** Validacao de dimensoes, tipos de dados primitivos, contagem de nulos e cardinalidade.
2. **Auditoria de Qualidade:** Deteccao de inconsistencias operacionais, verificacao de monotonicidade temporal e deteccao de mais de 18.000 outliers extremos na variavel `Amount` via metodo IQR ($3 \times IQR$).
3. **Limpeza e Tratamento:** Deduplicacao de registros e politicas de tratamento de valores discrepantes.
4. **Analise Exploratoria (EDA):** Analise de assimetria da variavel `Amount`, analise de densidade bivariada e separabilidade das componentes latentes de PCA ($V_1$ a $V_{28}$).
5. **Associacao Estatistica:** Correlacao linear (Pearson), nao-linear (Spearman) e correlacao ponto-bisserial com o target binario `Class`.
6. **Engenharia de Atributos:** Transformacao logaritmica em `Amount` para aproximacao normal e extracao de atributos temporais relativos.
7. **Pre-processamento sem Vazamento (*Leakage-Free*):** Encapsulamento com `ColumnTransformer` e `RobustScaler`, aplicando `fit` restrito aos dados de treino e `transform` nos dados de teste.
8. **Classificacao com k-NN e Otimizacao:** Busca em grade (`GridSearchCV`) para calibracao de $k$, esquema de ponderacao de vizinhos (*uniform* vs *distance*) e metricas de distancia.
9. **Benchmark Comparativo:** Comparacao multimodelo entre k-NN, Regressao Logistica e Random Forest sob curvas de Precisao-Revocacao (PR-AUC), F1-Score e matriz de confusao.
10. **Consolidacao:** Pipeline unificado pronto para inferencia com recomendacao tecnica de producao.

---

## Como Executar

```bash
jupyter notebook Lista_1_Antonio_Rodrigo_melhorado.ipynb
```
