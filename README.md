# FIA-REDES-NEURAIS
## Repositório destinado à entrega do trabalho de Fundamentos de Inteligência Artificial, com o tema: Classificação de Doenças Cardíacas
### PROBLEMATICA:
As doenças cardiovasculares causam, em média, a morte de pelo menos 400 mil brasileiros por ano, de acordo com a Agência Brasil e a Biblioteca Virtual em Saúde (BVS), sendo a doença mais mortal do território nacional e de nível mundial. A identificação antecipada dos fatores de risco é indispensável. À luz disso, o projeto se dedica a construir um classificador que indica a presença ou ausência desse condutor de falecimentos em níveis nacional e internacional.
### VISÃO GERAL
O dataset carregado (do arquivo heart.csv.csv) possui 1025 linhas e 14 colunas.
Com base na visualização dos dados, podemos classificar os atributos da seguinte forma:
## ATRIBUTOS 
## AGE
Descrição: A idade do paciente em anos.
Tipo: Contínua.
## trestbps (Pressão Arterial em Repouso)
Descrição: A pressão arterial sistólica do paciente em repouso, medida em mm Hg no momento da admissão hospitalar.
Tipo: Contínua.
## chol (Colesterol Sérico)
Descrição: A medição do colesterol sérico total do paciente, em mg/dl.
Tipo: Contínua.
## thalach (Frequência Cardíaca Máxima)
Descrição: A frequência cardíaca máxima atingida pelo paciente durante um teste de esforço (esteira).
Tipo: Contínua.
## oldpeak (Depressão do ST)
Descrição: Depressão do segmento ST induzida pelo exercício em relação ao repouso. Este é um indicador chave no eletrocardiograma (ECG) que mede a diferença no segmento ST antes e depois do exercício.
Tipo: Contínua (é a única variável float/decimal no dataset).
## sex (Sexo)
Descrição: O sexo biológico do paciente.
Valores: 1 = Masculino; 0 = Feminino.
## fbs (Açúcar no Sangue em Jejum)
Descrição: Indica se o nível de açúcar no sangue do paciente em jejum é superior a 120 mg/dl.
Valores: 1 = Verdadeiro (> 120 mg/dl); 0 = Falso (<= 120 mg/dl).
## exang (Angina Induzida por Exercício)
Descrição: Indica se o paciente sentiu angina (dor no peito) durante o teste de esforço.
Valores: 1 = Sim; 0 = Não.
## cp (Tipo de Dor no Peito)
Descrição: Classifica o tipo de dor no peito relatada pelo paciente. Este é um dos atributos mais importantes.
Valores:
0: Angina Típica (dor definitivamente relacionada ao coração, induzida por esforço).
1: Angina Atípica (dor no peito não típica de problemas cardíacos).
2: Dor Não-Anginosa (dor que não está relacionada à angina, como dor muscular).
3: Assintomático (paciente não relatou dor no peito).
## restecg (Resultados do ECG em Repouso)
Descrição: Os resultados do eletrocardiograma do paciente em repouso.
Valores:
0: Normal.
1: Anormalidade da onda ST-T (alterações que podem indicar problemas).
2: Hipertrofia ventricular esquerda provável ou definitiva (aumento do músculo cardíaco).
## slope (Inclinação do Segmento ST)
Descrição: Mede a inclinação do pico do segmento ST durante o exercício.
Valores:
0: Ascendente (Upsloping - o coração está se recuperando bem).
1: Plana (Flat).
2: Descendente (Downsloping - um forte indicador de isquemia).
## ca (Número de Vasos Principais Coloridos)
Descrição: O número de vasos sanguíneos principais (de 0 a 3) que apareceram coloridos (obstruídos) durante a fluoroscopia (um tipo de raio-X).
Valores: 0, 1, 2 ou 3.
## thal (Talassemia)
Descrição: Refere-se a um teste de estresse cardíaco com tálio, que verifica o fluxo sanguíneo para o coração.
Valores:
0: (Geralmente não usado ou remapeado. O notebook mostra que existe).
1: Normal (fluxo sanguíneo normal).
2: Defeito Fixo (uma área do coração que não tem fluxo sanguíneo, tanto em repouso quanto em exercício, geralmente de um infarto antigo).
3: Defeito Reversível (uma área que tem fluxo sanguíneo anormal durante o exercício, mas normaliza em repouso; indica um bloqueio).
## target (Alvo/Resultado)
Descrição: A variável que o modelo tentará prever.
Valores: 0 = Ausência de doença cardíaca; 1 = Presença de doença cardíaca.
### ANÁLISE DE PADRÕES DE VARIÁVEIS 
Os histogramas (gráficos de distribuição) das 10 primeiras variáveis mostram padrões importantes:
Distribuição Normal: As variáveis age (idade), trestbps (pressão arterial) e thalach (frequência cardíaca máx) têm uma distribuição que se assemelha a uma curva normal (formato de sino), que é o esperado para características biológicas.
Dados Assimétricos (Skewed):
chol (colesterol) apresenta uma assimetria à direita (right-skew), com uma "cauda" longa de valores mais altos, indicando a presença de alguns pacientes com colesterol muito acima da média.
oldpeak (depressão do ST) é fortemente assimétrico à direita. A grande maioria dos pacientes tem o valor 0 para esta medida.
Dados Categóricos Desbalanceados:
sex: O dataset possui significativamente mais pacientes do sexo masculino (1) do que feminino (0).
cp (tipo de dor): A maioria absoluta dos pacientes se concentra no tipo 0.
fbs (açúcar no sangue): A grande maioria dos pacientes não tem açúcar elevado em jejum (classe 0).
### ANÁLISE DE CORRELAÇÃO(HEATMAP)
A matriz de correlação (heatmap) é a ferramenta mais importante no notebook para entender quais atributos estão mais relacionados à presença de doença cardíaca (target).
Correlações Positivas com target: Valores mais próximos de +1 indicam que, quando o atributo aumenta, a chance de ter a doença (target=1) aumenta.
cp (0.43): O tipo de dor no peito é um forte indicador.
thalach (0.42): Uma frequência cardíaca máxima mais alta atingida no teste está associada à doença.
slope (0.35): A inclinação do segmento ST também é um indicador relevante.
Correlações Negativas com target: Valores mais próximos de -1 indicam que, quando o atributo aumenta, a chance de ter a doença (target=1) diminui.
exang (-0.44): A presença de angina induzida por exercício (valor 1) está fortemente ligada à ausência de doença.
oldpeak (-0.44): Valores baixos de depressão do ST estão associados à doença (valores altos estão associados à ausência dela).
ca (-0.39): Um número menor de vasos principais coloridos está ligado à doença.
thal (-0.34): O resultado do teste de tálio também é um forte preditor negativo.
Multicolinearidade (Preditor vs. Preditor): O notebook também nos permite ver se os próprios atributos preditores estão correlacionados (o que pode ser um problema para alguns modelos). As correlações mais fortes são oldpeak vs. slope (-0.58) e thalach vs. slope (0.40). Nenhuma delas é tão alta (ex: > 0.8) a ponto de ser um problema grave.
### ANÁLISE DE VALORES AUSENTES(INTERFERÊNCIA)
Não há valores ausentes no dataset.
### NORMALIZAÇÃO
Uma etapa crítica de pré-processamento identificada neste trabalho é a normalização dos dados. 
A ferramenta utilizada para isso é o StandardScaler da biblioteca Scikit-learn.O StandardScaler é um padronizador que aplica uma transformação estatística conhecida como Padronização (Standardization).A necessidade desta técnica é clara ao observar a análise de distribuição (vista nos histogramas): 
os atributos contínuos do dataset, como chol (colesterol, com valores de 120 a 550+) e oldpeak (depressão do ST, com valores de 0 a 6), existem em escalas numéricas muito diferentes.Algoritmos que calculam distâncias (como k-NN e SVM) ou que utilizam gradientes (como Regressão Logística) seriam enviesados por essas escalas. Eles dariam um peso desproporcional às variáveis com magnitudes maiores (como chol), independentemente de sua importância real para prever a doença cardíaca.Para corrigir isso, o StandardScaler padroniza cada atributo (feature) da seguinte forma:
Ele subtrai a média da coluna (µ) de cada valor (x).
Ele divide o resultado pelo desvio padrão da coluna (σ).
$$z = \frac{x - \mu}{\sigma}$$
z = (x - u)/σ
Isso transforma todos os atributos contínuos para que tenham uma média 0 e um desvio padrão 1. O resultado é um dataset onde todas as variáveis contribuem de forma justa e equilibrada para o treinamento do modelo, melhorando sua performance e estabilidade.
### CONTEÚDO
Dentro desse repositório está presente um arquivo (.ipynb) com todo código feito para o desenvolvimento do trablaho, comteplado com os passos, as visualizações e a análise dos resultados.
