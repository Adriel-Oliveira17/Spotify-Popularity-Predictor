# Spotify Popularity Predictor

Projeto de Ciência de Dados e Machine Learning para análise de músicas do Spotify e previsão de popularidade utilizando o algoritmo **Random Forest**.

---

## Objetivo

Investigar padrões presentes em faixas do Spotify e construir um modelo preditivo capaz de classificar se uma música possui potencial para ser considerada popular. 

A popularidade é estruturada como um problema de **classificação binária**:

* **Popular** -> Popularidade > 70
* **Não Popular** -> Popularidade <= 70

---

## Dataset

* **Dataset Utilizado**: [Spotify Tracks Dataset](https://www.kaggle.com/datasets/maharshipandya/-spotify-tracks-dataset) baixado via `kagglehub` (`maharshipandya/-spotify-tracks-dataset`).
* **Descrição**: Contém informações detalhadas sobre milhares de músicas, cobrindo atributos acústicos e metadados como:
  * `popularity`: Índice de popularidade da faixa (0 a 100).
  * `duration_ms`: Duração da música em milissegundos.
  * `explicit`: Indicador de conteúdo explícito (booleano).
  * `danceability`: Grau de dançabilidade da faixa.
  * `energy`: Medida percebida de intensidade e atividade.
  * `key`: Tom da música.
  * `loudness`: Volume geral da faixa em decibéis (dB).
  * `mode`: Modalidade harmônica (Maior / Menor).
  * `speechiness`: Presença de palavras faladas na faixa.
  * `acousticness`: Nível de acústica da música.
  * `instrumentalness`: Predição de ausência de vocais.
  * `liveness`: Presença de audiência/elementos ao vivo.
  * `valence`: Positividade/valência musical transmitida.
  * `tempo`: Andamento musical estimado em BPM.
  * `time_signature`: Fórmula de compasso estimada.
  * `track_genre`: Gênero musical da faixa.
  * `artists` & `track_name`: Nome dos artistas e da música.

---

## Etapas do Projeto

### 1. Limpeza e Tratamento dos Dados
* Download e carregamento do dataset direto do Kaggle via `kagglehub`.
* Remoção de valores ausentes (`dropna()`).
* Remoção de registros duplicados (`drop_duplicates()`).
* Remoção de colunas que não agregam valor preditivo à modelagem: `Unnamed: 0`, `track_id` e `album_name`.

### 2. Análise Exploratória de Dados (EDA)
Realização de análises estatísticas e visuais para compreender os fatores que influenciam a popularidade:
* Resumo estatístico de popularidade média, máxima e contagem agrupado por gênero musical (`track_genre`).
* Identificação de gêneros com maior média de popularidade (ex.: *pop-film*, *k-pop*, *chill*, *sad*, *grunge*) e menor média (ex.: *iranian*, *romance*, *latin*).
* Análise de correlação entre as variáveis musicais acústicas e a popularidade.
* Comparação da popularidade entre músicas explícitas e não explícitas.
* Ranking dos artistas e das faixas mais populares do dataset.

### 3. Engenharia de Features
* Criação da variável alvo `target` (binária) baseada no limiar de popularidade (> 60).
* Conversão da variável booleana `explicit` para o formato numérico `explicit_value`.

### 4. Machine Learning
* **Algoritmo**: `Random Forest Classifier`
* **Features de Entrada (Preditores)**:
  * `duration_ms`
  * `danceability`
  * `energy`
  * `loudness`
  * `mode`
  * `liveness`
  * `valence`
  * `tempo`
  * `time_signature`
  * `explicit_value`
* **Variável Alvo**: `target` (1 = Popular, 0 = Não Popular)

* 
### 5. Validação do Modelo
* **Holdout Validation**: Divisão do conjunto de dados em 85% para treino e 15% para teste via `train_test_split`.
* **Estratificação (`stratify`)**: Manutenção da proporção das classes da variável alvo entre os dados de treino e teste.
* **Ajuste de Pesos (`class_weight='balanced'`)**: Tratamento do desbalanceamento de classes no algoritmo Random Forest.
* **Métricas de Desempenho**: Avaliação do modelo no conjunto de teste via `classification_report` (Precisão, Recall, F1-Score e Acurácia).

---

## Tecnologias Utilizadas

* **Linguagem**: Python
* **Manipulação de Dados**: Pandas, NumPy
* **Visualização de Dados**: Matplotlib, Seaborn
* **Machine Learning**: Scikit-Learn
* **Download de Datasets**: KaggleHub

---

## Resultados

* O modelo **Random Forest** foi capaz de capturar padrões complexos não lineares entre os atributos acústicos e a popularidade das faixas.
* A utilização de validação cruzada garantiu estabilidade na capacidade de generalização do modelo frente a novos dados.

---

## Exemplo de Predição

O modelo aceita um vetor numérico contendo os atributos acústicos e gerais da faixa:

```python
# Exemplo de entrada (features de uma música):
# [duration_ms, danceability, energy, loudness, mode, liveness, valence, tempo, time_signature, explicit_value]
amostra = [[230666, 0.676, 0.461, -6.746, 1, 0.358, 0.715, 87.917, 4, 0]]

# Previsão do modelo:
# Saída: 1 (Popular) ou 0 (Não Popular)
