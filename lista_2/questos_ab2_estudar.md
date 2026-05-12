# Questões de Prova - Ciência de Dados

# 1. Em que tipos de problema é mais adequado usar Regressão Linear Múltipla e Regressão Logística? (2 pontos)

### Rascunho

- Regressão Linear Múltipla(Número continuo (exato)): Para problemas onde queremos prever um número contínuo, um número exato. Por exemplo: Prever o preço exato da cotação de uma ação. Um Hiperplano que tentar cortar o espaço passando o mais perto possível de todos os planos

- Regressão Logística(Classificação): Serve para resolver problemas de predição de uma categoria. Exemplo: Esse fundo imobiliaria vai pagar dividentos acima da média esse mês? sim ou não. Ela pega o calculo da linear e joga em uma função SIgmoide. Amassando a reta e transformando em uma curva S, para se moldar aos dados e separar as classes acima e abaixo do S
r

## **-=- Resposta -=-** 

É mais adequado usar a Regressão Linear Múltipla em problemas que exigem a previsão de uma variável contínua (ex: prever valores financeiros, temperatura, vendas). Já a Regressão Logística é adequada para problemas de classificação, onde o objetivo é prever probabilidades ou categorizar dados em classes discretas (ex: sim/não, fraude/autêntico).

--- 

# 2. Qual a importância do classificador Árvore de Decisão para a interpretação dos dados? (2 pontos)

### Rascunhoc

Pelo que entendo, classificaodr Arvore de decisão é ótimo para explicabilidade pq ele mostra a arvore bonitinha e as divisão de grupos. Ele dá os caminhos de cada pessoas no decorrer da árvore sendo simples de explicar por que uma pessoa está no grupo x ou y


## **-=- Resposta -=-** 

A principal importância do classificador Árvore de Decisão para a interpretação dos dados é a sua alta explicabilidade. Por ser um modelo que gera regras lógicas visuais, ele permite que o analista compreenda de forma transparente quais atributos foram mais importantes para dividir os dados e qual caminho o algoritmo tomou para chegar à decisão final.

--- 

# 3. Descreva cada um dos componentes de uma Série Temporal. (2 pontos)

### Rascunho
São 4 camadas
1. Tendência(trend): Tendência é quase como a definiçã de tendencia, se por algo do hype, tá com tendencia alta aquele assunto ta em crescimento. Por exemplo, a palavra "Hardness" esta em alta, com crescimento elevado devido a IA. mas isso daqui Seria a LONGO PRAZO
2. SAZONALIDADE: que loucura, esse daqui funciona basicamente como periodos fixos e conhecidos. Pensa da seguinte forma: no natal os panetones vendem pra cacete no natal e essa seria a sazonalidade, então tem frequencia de 12 meses por exemplo
3. Ciclicidade: É quando há uma alta/baixa onde a e sem perido Fixo, por exemplo, Sanozaldiade o panetone sempre no natal, MAS a bolha da IA começou e não tem périodo fixo pra acabar. Mas em certo dias os investidores veem que as startups não está trazendo retorno e acabam parando de investir, uma queda real, normal e que acontece. E acabar com a bolha da IA, não tem périodo fixo, mas no momento está em alta
4. Ruído: Seria o ruído do mundo real, algo inesperado, que acontece no dia a dia. Por exemplo uma empresa demite 300 pessoas devido a IA, ela posta no twitter e as ações caem drasticamente. Uma canetada de um politico


## **-=- Resposta -=-** 

Uma Série Temporal é composta por quatro elementos principais: Tendência (o movimento e direção de longo prazo dos dados), Sazonalidade (padrões de flutuação que se repetem em intervalos fixos e regulares de tempo), Ciclicidade (flutuações de longo prazo sem período fixo, geralmente ligadas a fatores macroeconômicos) e o Ruído ou Fator Irregular (variações aleatórias, imprevisíveis e de curto prazo que não seguem nenhum padrão).

--- 

# 4. Mostre a importância de se utilizar a abordagem de Meta-aprendizado como ferramenta para descoberta de informação. (2 pontos)

### Rascunho

Oxe que brabo, ela é muito importante pq facilida nossa vida, abordagens de meta aprendizagem dizem para utializar o conhecimemento que já temos com problemas passados. A abordagem faz uma analise da base, não completa mais em pedaços para entender o dataset como um todo. Ela analisa caractericias do novo problema e propoe uma algoritmo novo e hiperparametros mais eficientes automaticamente. facilita dms a vida slkkk


## **-=- Resposta -=-** 

A importância do Meta-aprendizado como ferramenta de descoberta de informação está na sua capacidade de automatizar e acelerar a extração de conhecimento. Ao utilizar a experiência adquirida em tarefas e bases de dados anteriores, o meta-aprendizado analisa as características do novo problema (meta-features) para recomendar os algoritmos e hiperparâmetros mais eficientes de forma automática. Isso permite uma adaptação rápida a cenários desconhecidos, economizando tempo computacional e exigindo um volume muito menor de dados para gerar insights precisos.

--- 

# 5. Qual é a importância de Visualização de Dados para um cientista de dados (2 pontos)

### Rascunho

Extremamente importante na verdade. Pq não tem como mostrar um bloco com milhares de números, tem que deixar tudo organizando e podemos fazer isso com um gráfico por exemplo. Onde vizualizar dados ajuda a ter insights, tomada de decisão e ajuda a traduzir pra storytelling e comunicação. Para o ciêncista de dados é essencial. pois sendo bem sincero, vizualizar os dados ajudam a ter insights valiosos por exemplos "EM hora x as pessoas compram menos e se lancassemos uma promoção relampago esse hroario toda vez?" insight, tomada de decisão e comunição. tudo isso em uma simples frase VAI TOMANDO PORRA


## **-=- Resposta -=-** 

A importância fundamental da Visualização de Dados para um cientista de dados reside na capacidade de traduzir grandes volumes de dados complexos em representações visuais acessíveis. Isso agiliza a fase de Análise Exploratória (identificação de padrões, tendências e outliers). Além disso, atua como a ferramenta central de Data Storytelling, permitindo a comunicação clara de insights técnicos para profissionais de outras áreas (stakeholders), o que é essencial para embasar a tomada de decisões estratégicas.

--- 

# 6. Com relação ao método Máquina de Vetores de Suporte (SVM), mostre duas formas de otimizar seus parâmetros. (2 pontos)


### Rascunho

SVM É UM CLASSIFICADOR, que monta um hiperplano onde vai tentar categorizar a base, tentando se moldar para atingir o objetivo de classificação. Mas para ele ficar bom precisa do hiper parametros corretos e usaremos o grid search e ele busca em grid kk que é um brute force de varios valores até achar o melhor. E O RANDOM search ele é um brute force mais limitado onde aqui vc define os limites e ele vai aleatoriamente!


## **-=- Resposta -=-** 

Duas formas principais de otimizar os hiperparâmetros de um SVM (como $C$ e $\gamma$) são:
1. Grid Search: Realiza uma busca exaustiva, testando todas as combinações possíveis dentro de uma grade de valores pré-definida pelo usuário. É rigoroso, mas computacionalmente custoso.
2. Random Search: Sorteia e avalia combinações aleatórias de parâmetros dentro de um intervalo definido. É computacionalmente mais eficiente e frequentemente encontra resultados ótimos em uma fração do tempo do Grid Search.

--- 

# 7. Quais tipos de problemas são preferíveis utilizar Naive Bayes? (2 pontos)

### Rascunho

o NAIVE bayes eu sei que ele é ingenuo. Ele é calcula de maneira independete e depois multiplica. Mas no geral o naive bayes é ótimo texto mesmo SPAM eu conheço o carro chefe, no geral tá ótimo


## **-=- Resposta -=-** 

O classificador Naive Bayes é preferível em problemas de classificação de texto e processamento de linguagem natural (NLP), como filtragem de spam e análise de sentimentos. Além disso, por possuir um custo computacional extremamente baixo e ser treinado de forma rápida, é altamente recomendado para predições em tempo real e para datasets com alta dimensionalidade (muitas features independentes).

--- 

# 8. Crie um conjunto de dados com 2 classes para mostrar:
   a. Uma classificação após usar Árvore de Decisão. (1 ponto)
   b. Uma regra gerada pela árvore (use pelo menos 2 atributos). (1 ponto)

### Rascunho

Ativos, setor, valor, dividendo, comprar

acai 2, Eletrico, 100, 5, SIM
ação 1, Artistico, 110, 1.2, não

Basicamente fazer algumas comparações
pra vê se a ação vale a pena comprar, 

acao 3, seria do setor de Elétrico é 100 reais e paga 6, logo vale a pena comprar

b)

SE (Setor == Elétrico) E (Dividendo >= 5) ENTÃO Comprar = SIM.





## **-=- Resposta -=-** 

Ativo,   Setor,      P/VP (Preço/Valor Patrimonial),  Dividend Yield (DY), Classe (Comprar?)
Ação A,  Elétrico,            0.9,                       10%,                 Sim
FII B,   Laje Corporativa,    1.2,                       6%,                  Não
Ação C,  Varejo,              1.5,                       4%,                  Não
FII D,   Papel,               0.85,                      12%,                 Sim
Ação E,  Elétrico,             1.3,                      8%,                  Não


a. Uma classificação após usar a Árvore de Decisão (1 ponto)
Imagine que um ativo novo acabou de entrar no radar da nossa IA:

Novo Ativo: Ação F

Setor: Elétrico

P/VP: 0.88

DY: 11%

Classificação: Após passar pela nossa Árvore de Decisão treinada com o conjunto acima, a Ação F cai no nó final e recebe a classificação Classe = Sim (Comprar).

b. Uma regra gerada pela árvore usando pelo menos 2 atributos (1 ponto)
Para chegar nessa classificação da Ação F, a árvore gerou e seguiu uma regra lógica muito clara cruzando dois atributos do nosso dataset. A regra extraída é:

Regra de Decisão:
SE (Setor == "Elétrico") E (P/VP < 1.0) ENTÃO Classe = "Sim" (Comprar).

--- 

# 9. Com relação aos métodos Rede Neural de Camada Única (Perceptron) e Máquina de Vetores de Suporte (SVM), descreva:
   a. Que tipos de problemas eles podem resolver em comum. (1 ponto)

   b. A principal vantagem do SVM sobre o Perceptron (exemplifique). (1 ponto)

### Rascunho

Ambos foram criados para classificação binaria de dados linearmente separaveis. Mas o Perceptron ele fica colado no dado de uns dos grupos

e o SVM que é parceiro aqui no canal então ele faz o seguinte. AO invez de fazer uma reta COLADA em um dado, ele tem uma margem de segunraça pois ele faz exatamente no cenotro do vão.

por exemplo duas cidades A E B


o svm se for sugerir fazer um rodovida ele falaria "no meio do descampando entre as cidades" e o perceptron ele faria " faz ali colada no mudo da primeira cada da cidade A


## **-=- Resposta -=-** 

a. Em comum, ambos são utilizados para resolver problemas de classificação binária em dados linearmente separáveis (traçando um hiperplano linear de separação).

b. A principal vantagem do SVM é a busca pelo hiperplano de margem máxima, que garante uma melhor generalização para novos dados. Exemplo: Enquanto o Perceptron pode traçar uma reta muito próxima a uma das classes (arriscando errar predições futuras), o SVM posiciona a reta de separação com a maior distância segura possível entre os pontos extremos (vetores de suporte) de ambas as classes. Além disso, o SVM pode usar funções de Kernel para resolver problemas não-lineares, algo impossível para um Perceptron de camada única.

--- 

# 10. De que forma modelos para séries temporais podem ajudar na descoberta de informação? (2 pontos)

### Rascunho

Para muitos na vdd pq as séries temporais são dividias em 4 partes tedencia, sazonalidade, ciclicidade e ruido. Todas presente no mundo real

a tendencia pode nos ajudar a entender os dados a longo prazo

o sazonalidade ajuda entender picos esperados, feriados, por exemplo

ciclicidade ajuda a entender periodo não fixos do dataset, situações que fazem sentindo, mas com o decorrer do tempo deixaram de fazer

ruído ajuda a mostrar como escolhas do mundo real influencia nos dados

vizualizar os dados dessas forma ajuda muito

No geral vai ajudar a entender os padrões e assim descorbir informações

tudo isso permite fazer Forecasting (previsões de mercado) e Detecção de Anomalias


## **-=- Resposta -=-** 

Os modelos para séries temporais ajudam na descoberta de informação ao analisar dados estruturados cronologicamente para extrair padrões que dependem do tempo. Sua principal contribuição se dá em três frentes: 1. Previsão (Forecasting) de cenários e valores futuros com base no histórico; 2. Detecção de Anomalias, identificando rapidamente ruídos, fraudes ou comportamentos atípicos que fogem do padrão; e 3. Identificação de Tendências e Sazonalidade, revelando ciclos ocultos e movimentos de longo prazo que não seriam descobertos em análises estáticas.

--- 


# 11. Sobre Árvores de Decisão, descreva três vantagens de usar esse método. (1 ponto)

### Rascunho

1. Explicabilidade (vizualizaçao de dados): Muito bom para intepretar dados
2. Exige pouco pré-processamento: não precisa de normalizaão, ela lida naturalmente com a mistura de variáveis numéricas e categóricas
3. Seleção Automática de Atributos: ele já identifica os atritutos mais relevantes para o problema


## **-=- Resposta -=-** 

1. Alta Interpretabilidade: É um modelo "caixa-branca" baseado em regras simples (SE-ENTÃO), facilitando a compreensão humana.
2. Menor necessidade de preparação de dados: Lida naturalmente com a mistura de variáveis numéricas e categóricas, não exigindo normalização ou padronização complexa dos dados.
3. Seleção de atributos embutida: O próprio algoritmo identifica e prioriza as variáveis mais relevantes para o problema, colocando-as no topo da estrutura e ignorando dados irrelevantes.

--- 

# 12. Mostre como o classificador Random Forest pode ser usado para extração de informações a partir de um conjunto de dados. (1 ponto)

### Rascunho

Importância dos Atributos (Feature Importance).

O modelo analisou todos os dados e revelou que P/VP e Vacância são os verdadeiros motores da decisão. O resto tem impacto mínimo.

tá porra o random florest dá a variavel mais importante. no caso quais tem maior decisão para o problema


## **-=- Resposta -=-** 

O classificador Random Forest é utilizado na extração de informações principalmente através da métrica de Importância de Atributos (Feature Importance). Ao combinar múltiplas árvores de decisão, o algoritmo consegue calcular e ranquear estatisticamente quais variáveis da base de dados têm o maior peso e poder de decisão para o problema. Isso permite extrair o conhecimento de quais fatores são realmente cruciais na vida real, facilitando a eliminação de ruídos e a compreensão profunda do conjunto de dados.

--- 
 
# 13. Mostre como um sistema usando a abordagem de Meta-aprendizado pode ajudar: a. Empresas (1 ponto)  b. Usuários (1 ponto)

### Rascunho

a) Empresas: Reduz drasticamente o tempo e o custo computacional de desenvolvimento, pois o sistema utiliza a experiência de aprendizado prévia para se adaptar rapidamente a novos problemas, exigindo um volume muito menor de dados na entrada.
b) Usuários: O sistema consegue mapear os gostos e necessidades do usuário com pouquíssimas interações iniciais, eliminando o atrito de configurações longas e manuais.

## **-=- Resposta -=-** 

a. Empresas (1 ponto): Ajuda reduzindo drasticamente os custos de processamento e o tempo de desenvolvimento (time-to-market). Permite a criação de soluções eficientes exigindo uma quantidade muito menor de novos dados (few-shot learning), pois o sistema reaproveita o conhecimento extraído de tarefas anteriores.

b. Usuários (1 ponto): Ajuda proporcionando uma experiência altamente personalizada e fluida de forma quase imediata. O sistema consegue se adaptar rapidamente aos hábitos e preferências do usuário com pouquíssimas interações, eliminando atritos e longos processos de configuração inicial (mitigando o problema do cold-start).

--- 

# 14. Descreva um sistema de Meta-aprendizado (explicando a construção de meta-características, meta-base e meta-aprendiz) usado para recomendar hiperparâmetros do modelo ARIMA. (2 pontos)

### Rascunho


## **-=- Resposta -=-** 

--- 

# 16. Sobre Visualização de Dados, descreva cada uma das seis etapas recomendadas para uma boa apresentação de resultados. (2 pontos)

### Rascunho


## **-=- Resposta -=-** 

--- 

# 17. Cite 3 vantagens de utilizar o classificador Árvore de Decisão para a análise dos dados? (2 pontos)

### Rascunho


## **-=- Resposta -=-** 

--- 

# 18. Descreva a importância de cada um dos parâmetros de uma Rede Neural: número de camadas escondidas, função de ativação e taxa de aprendizagem. (2 pontos)

### Rascunho


## **-=- Resposta -=-** 

--- 

# 19. Supondo que você é $um(a)$ cientista de dados em uma empresa, descreva como você poderia utilizar Meta-aprendizado para economizar tempo e/ou dinheiro dessa empresa. (2 pontos)

### Rascunho


## **-=- Resposta -=-** 

--- 

# 20. No contexto de Visualização de Dados, mostre formas de melhorar o engajamento do público. (2 pontos)

### Rascunho


## **-=- Resposta -=-** 

--- 

# 20. Descreva três vantagens da utilização de Árvores de Decisão quando comparando com o k-NN. (1 ponto)

### Rascunho


## **-=- Resposta -=-** 

--- 

# 21. Supondo que você está responsável pela aplicação de Redes Neurais para identificar se um paciente tem ou não COVID a partir de dados de pacientes, descreva um passo a passo de como você iria encontrar a melhor configuração de Rede Neural que se adeque ao problema. (2 pontos)

### Rascunho


## **-=- Resposta -=-** 

--- 




Dado que já mostrei queria começar a analisar isso
pegar  oresulto da llm 

texto para 3 partes dessas issue

pega a embbeding de cada parte de texto

analisar





componetizar oq eu fiz





