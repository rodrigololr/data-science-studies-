# Projeto Final de Ciencia de Dados - Analise de Microdados de Seguranca Publica (CVLI Alagoas)

Projeto de analise estatistica, mineracao de padroes e modelagem orientada a dados a partir dos microdados oficiais de **Crimes Violentos Letais Intencionais (CVLI)** registrados pela Secretaria de Seguranca Publica do Estado de Alagoas no periodo de **2012 a abril de 2026**.

---

## Proposta e Objetivo

O objetivo deste projeto e aplicar metodologias completas de Ciencia de Dados para:
1. Compreender a dinamica temporal e geografica da violencia letal no Estado de Alagoas.
2. Identificar fatores determinantes, sazonalidades, correlacoes e padroes de vulnerabilidade demografica das vitimas.
3. Apoiar a formulacao de politicas publicas de seguranca baseadas em evidencias (*Data-Driven Public Policy*).
4. Estruturar as conclusoes tecnicas em formato executivo de *Pitch*, comunicando de forma clara o diagnostico e as recomendacoes de intervencao.

---

## Dicionario dos Microdados (`cvli-microdados-alagoas-2012-a-abril-de-2026.csv`)

| Atributo | Descricao | Tipo | Relevancia Analitica |
|---|---|---|---|
| `ID_CONTROLE` | Identificador unico do registro | Numerico | Chave primaria de rastreamento |
| `SUBJETIVIDADE` | Categoria principal do delito | Categorico | Tipificacao penal (ex: CVLI) |
| `SUBJETIVIDADE COMPLEMENTAR` | Classificacao especifica | Categorico | Homicidio doloso, latrocinio, lesao corporal seguida de morte |
| `DATA DO FATO` | Data da ocorrencia | Data (`DD/MM/AAAA`) | Analise de series temporais e evolucao anual/mensal |
| `HORA DO FATO` | Horario estimado do evento | Horario (`HH:MM`) | Analise de sazonalidade horaria e turnos criticos |
| `CIDADE DO FATO` | Municipio de ocorrencia | Categorico | Distribuicao espacial e concentracao geografica |
| `BAIRRO DO FATO` | Bairro ou localidade | Categorico | Mapeamento intra-urbano e identificacao de manchas criminais |
| `SEXO DA VITIMA` | Genero da vitima | Categorico | Perfil epidemiologico de genero |
| `COR/RACA DA VITIMA` | Autodeclaracao / Laudo pericial | Categorico | Analise de vulnerabilidade racial e recorte social |
| `IDADE DA VITIMA` | Idade em anos | Numerico | Analise geracional e vitimizacao juvenil |
| `INSTRUMENTO UTILIZADO` | Meio empregado no crime | Categorico | Arma de fogo (PAF), arma branca, espancamento, etc. |
| `LOCAL DO FATO` | Tipologia do ambiente | Categorico | Via publica, residencia, estabelecimento comercial |
| `OCUPACAO VITIMA` | Ocupacao profissional informada | Categorico | Fator socioeconomico complementar |
| `ESCOLARIDADE VITIMA` | Nivel de instrucao formal | Categorico | Grau de escolarizacao das vitimas |

---

## Dimensoes Metodologicas de Analise

1. **Analise Temporal:**
   - Tendencias historicas no intervalo 2012-2026.
   - Decomposicao sazonal (dias da semana, fins de semana, feriados e faixas de horario).
2. **Analise Geoespacial e Territorial:**
   - Concentracao municipal (comparativo capital vs interior).
   - Mapeamento de manchas criminais nos bairros de maior incidencia.
3. **Perfil Epidemiologico e Demografico:**
   - Piramides etarias de vitimizacao e desproporcao por genero e raca.
   - Cruzamento entre tipologia do local e instrumento utilizado.
4. **Modelagem & Recomendacoes Estrategicas:**
   - Identificacao de padroes associativos entre horario, local e meio empregado para direcionamento inteligente de patrulhamento ostensivo.

---

## Documentos de Apoio

- `descricao_projeto.md`: Proposta detalhada, requisitos tecnicos e instrucoes para estruturacao da apresentacao em formato de pitch.
- `Projeto (2026-1).pdf`: Edital institucional e barema de avaliacao da disciplina de Ciencia de Dados (IC/UFAL).
