# FIA-REDES-NEURAIS
## Repositório destinado à entrega do trabalho de Fundamentos de Inteligência Artificial, com o tema: Classificação de Doenças Cardíacas
### PROBLEMATICA:
As doenças cardiovasculares causam, em média, a morte de pelo menos 400 mil brasileiros por ano, de acordo com a Agência Brasil e a Biblioteca Virtual em Saúde (BVS), sendo a doença mais mortal do território nacional e de nível mundial. A identificação antecipada dos fatores de risco é indispensável. À luz disso, o projeto se dedica a construir um classificador que indica a presença ou ausência desse condutor de falecimentos em níveis nacional e internacional.
### 📁 CONTEÚDO 
Notebook (.ipynb) com todo o desenvolvimento do modelo;

Dataset original (heart.csv);

Arquivo de pesos treinados (best_model_improved.weights.h5);

Documentação e análise dos resultados obtidos.

### 📊 VISÃO GERAL DO DATASET
1025 linhas

14 atributos (idade, sexo, pressão arterial, colesterol, frequência cardíaca máxima etc.)

1 variável alvo (target):

0 → ausência de doença cardíaca

1 → presença de doença cardíaca
## 🎯 target (Alvo/Resultado)
A variável que o modelo tentará prever.

Valores: 0 = Ausência de doença cardíaca;

1 = Presença de doença cardíaca.
### 🔍 ANÁLISE DE PADRÕES DE VARIÁVEIS 
Os histogramas mostraram três tipos principais de comportamento nas variáveis do dataset. Algumas, como age, trestbps e thalach, apresentaram distribuição próxima da normal, o que é comum em medidas biológicas. Outras variáveis exibiram assimetria à direita, como chol, que possui alguns valores muito altos, e oldpeak, em que a maioria dos pacientes tem valor 0.
Também foi possível observar desbalanceamento em variáveis categóricas, especialmente em sex (predominância de homens), cp (maioria absoluta na classe 0) e fbs (quase todos com valor 0).

### 🔍 ANÁLISE DE CORRELAÇÃO(HEATMAP)
A matriz de correlação evidenciou quais atributos têm relação mais forte com o alvo. Entre as correlações positivas, destacam-se cp (0.43), thalach (0.42) e slope (0.35), indicando que valores maiores tendem a estar associados à presença da doença.
Já as correlações negativas mais relevantes foram exang (-0.44), oldpeak (-0.44), ca (-0.39) e thal (-0.34), sugerindo que seus valores elevados estão ligados à ausência da condição cardíaca.
A análise também verificou multicolinearidade entre preditores: as relações mais fortes foram oldpeak × slope (-0.58) e thalach × slope (0.40), mas nenhuma intensa o suficiente para prejudicar o modelo.

### NORMALIZAÇÃO
A normalização foi uma etapa essencial, realizada com o StandardScaler, que aplica padronização estatística. Isso foi necessário devido às grandes diferenças de escala entre variáveis contínuas, como chol (valores altos) e oldpeak (valores baixos).
Sem essa padronização, modelos baseados em distância ou gradiente seriam influenciados de forma injusta pelas variáveis de maior magnitude. O StandardScaler transforma cada valor para:

$$
z = \frac{x - \mu}{\sigma}
$$

​


garantindo que todas as variáveis tenham média 0 e desvio padrão 1. Assim, contribuem de maneira equilibrada no treinamento, aumentando a estabilidade e o desempenho do modelo.

### CONCLUSÃO 
A acurácia de 92% alcançada pelo modelo com os dados normalizados não apenas valida a escolha da arquitetura da Rede Neural Artificial, mas também demonstra um potencial significativo para auxiliar na triagem e no diagnóstico precoce de doenças cardíacas. A normalização dos dados foi um fator decisivo, não só por otimizar o processo de treinamento e garantir a estabilidade do modelo, mas também por aumentar a robustez e a capacidade de generalização do modelo para dados futuros e não vistos. Em um cenário real, onde a consistência e a confiabilidade são cruciais, essa capacidade de generalização é tão importante quanto a acurácia bruta, pois assegura que o modelo manterá seu bom desempenho mesmo com novas informações.

![resultadoFIA](https://github.com/user-attachments/assets/a45a0cc0-bcf1-4381-a876-6f4c4e091c3b)

Matriz de Confusão: Distribuição dos Acertos e Erros
A matriz de confusão apresenta a contagem real das previsões:

Verdadeiros Positivos (VP = 100): O modelo identificou corretamente 100 pacientes que, de fato, tinham a doença (Com Doença (1)).

Verdadeiros Negativos (VN = 90): O modelo identificou corretamente 90 pacientes que, de fato, não tinham a doença (Sem Doença (0)).

Falsos Negativos (FN = 5): Este é o erro mais crítico no diagnóstico. O modelo deixou de detectar a doença em apenas 5 pacientes (classificando-os incorretamente como 'Sem Doença').

Falsos Positivos (FP = 10): O modelo classificou erroneamente 10 pacientes como tendo a doença quando, na verdade, não tinham.


