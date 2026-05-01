# Revisão técnica do notebook

Arquivo analisado: [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb)
Data da revisão: 05/04/2026

## Resumo executivo

A estrutura geral do trabalho está boa e cobre as etapas esperadas. Porém, há inconsistências importantes de pipeline e validação que podem afetar a correção técnica e a nota, principalmente nas Questões 7, 8, 9 e 10.

---

## Achados por gravidade

## 1) Grave

1. Treino e inferência usam representações diferentes dos dados

- O KNN final é treinado com dados não transformados em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L1473), chamado em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L1477).
- A inferência final transforma os dados com preprocessador robusto antes de prever em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L1658).
- Impacto: o modelo recebe na predição um espaço de atributos diferente daquele usado no treino.

2. Comparação da Questão 9 fica tecnicamente inconsistente no cenário KNN tratado

- Treino do KNN tratado com X sem transformação em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L1555).
- Predição com X de teste transformado em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L1556), usando transformação criada em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L1570).
- Impacto: as métricas desse cenário não representam pipeline válido de ponta a ponta.

## 2) Alta

3. Vazamento de informação na Questão 7

- Preprocessadores são ajustados com fit_transform no conjunto inteiro em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L1285) e [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L1286).
- O enunciado pede prevenção de leakage; ajuste deveria ser apenas no treino.

4. Questão 9 não cobre totalmente o enunciado

- Tempo de predição do Random Forest é calculado em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L1564), mas não é reportado no dataframe final em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L1565).
- Falta perfil de erro detalhado (por exemplo FP, FN, matriz de confusão) para comparação operacional dos modelos.

## 3) Média

5. Conclusão da Questão 10 está em branco

- Marcador sem preenchimento em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L1685) e [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L1686).

6. Questões 1 e 2 estão definidas, mas sem chamada explícita

- Definições em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L442) e [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L554).
- Não há execução explícita dessas funções no fluxo, o que reduz reprodutibilidade da narrativa.

7. Relatório da auditoria da Questão 2 tem mensagens fixas

- Linhas fixas de status em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L586) e [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L587).
- A linha de valores implausíveis menciona Amount e Time, mas usa apenas contador de Amount em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L585).

8. Questão 3 declara comparação de estratégias, mas não mostra evidência no output

- Cálculos existem em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L684) e [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L685).
- Impressões comparativas estão comentadas em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L686) e [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L687).

## 4) Baixa

9. Engenharia temporal da Questão 6 está praticamente inativa no fluxo

- Time removida na limpeza em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L677).
- Atributo Hour só é criado se Time existir em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L1138).
- Impacto: esse sinal temporal pode não estar contribuindo como esperado.

10. Justificativa da distância Manhattan está fixa no texto

- Mensagem fixa em [Lista_1_Antônio_Rodrigo_completa.ipynb](Lista_1_Antônio_Rodrigo_completa.ipynb#L1463).
- Em eventual rerun com outro melhor modelo, texto pode ficar inconsistente com o resultado.

---

## Observação de execução

No ambiente atual, as células aparecem como não executadas na sessão do VS Code, apesar de haver outputs salvos no arquivo. Para garantir robustez na avaliação, recomenda-se rodar o notebook do início ao fim antes da entrega.

---

## Prioridade recomendada de correção

1. Corrigir consistência de pipeline entre treino, teste e inferência (Q7, Q8, Q9, Q10).
2. Eliminar leakage no preprocessamento (Q7).
3. Completar Q9 com tempo e perfil de erro por modelo.
4. Preencher conclusão da Q10.
5. Tornar Q1 e Q2 explicitamente executadas e ajustar mensagens fixas da auditoria.
6. Exibir evidência da comparação de estratégias na Q3.
