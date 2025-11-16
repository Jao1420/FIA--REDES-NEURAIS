# FIA-REDES-NEURAIS
## Repositório destinado à entrega do trabalho de Fundamentos de Inteligência Artificial, com o tema: Classificação de Doenças Cardíacas
### PROBLEMATICA:
As doenças cardiovasculares causam, em média, a morte de pelo menos 400 mil brasileiros por ano, de acordo com a Agência Brasil e a Biblioteca Virtual em Saúde (BVS), sendo a doença mais mortal do território nacional e de nível mundial. A identificação antecipada dos fatores de risco é indispensável. À luz disso, o projeto se dedica a construir um classificador que indica a presença ou ausência desse condutor de falecimentos em níveis nacional e internacional.
### CONTEÚDO
Dentro desse repositório está presente um arquivo (.ipynb) com todo código feito para o desenvolvimento do trabalho, comteplado com os passos, as visualizações e a análise dos resultados.

### VISÃO GERAL
O dataset carregado (do arquivo heart.csv.csv) possui 1025 linhas e 14 colunas.
Com base na visualização dos dados, podemos classificar os atributos da seguinte forma:
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

### NORMALIZAÇÃO
Uma etapa crítica de pré-processamento identificada neste trabalho é a normalização dos dados. 
A ferramenta utilizada para isso é o StandardScaler da biblioteca Scikit-learn.O StandardScaler é um padronizador que aplica uma transformação estatística conhecida como Padronização (Standardization).A necessidade desta técnica é clara ao observar a análise de distribuição (vista nos histogramas): 
os atributos contínuos do dataset, como chol (colesterol, com valores de 120 a 550+) e oldpeak (depressão do ST, com valores de 0 a 6), existem em escalas numéricas muito diferentes.Algoritmos que calculam distâncias (como k-NN e SVM) ou que utilizam gradientes (como Regressão Logística) seriam enviesados por essas escalas. Eles dariam um peso desproporcional às variáveis com magnitudes maiores (como chol), independentemente de sua importância real para prever a doença cardíaca.Para corrigir isso, o StandardScaler padroniza cada atributo (feature) da seguinte forma:
Ele subtrai a média da coluna (µ) de cada valor (x).
Ele divide o resultado pelo desvio padrão da coluna (σ).
$$z = \frac{x - \mu}{\sigma}$$
z = (x - u)/σ
Isso transforma todos os atributos contínuos para que tenham uma média 0 e um desvio padrão 1. O resultado é um dataset onde todas as variáveis contribuem de forma justa e equilibrada para o treinamento do modelo, melhorando sua performance e estabilidade.

