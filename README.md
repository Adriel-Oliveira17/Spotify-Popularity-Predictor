# Spotify Popularity Predictor

Projeto de Ciência de Dados e Machine Learning para análise de músicas do Spotify e previsão de popularidade utilizando Random Forest.

## Objetivo

Investigar padrões presentes em músicas do Spotify e construir um modelo capaz de prever se uma faixa possui potencial para ser considerada popular.

A popularidade é transformada em um problema de classificação binária:

- Popular → Popularidade > 60
- Não Popular → Popularidade ≤ 60

---

## Dataset

Dataset utilizado:

Spotify Tracks Dataset

Contém informações sobre milhares de músicas, incluindo:

- Popularidade
- Danceability
- Energy
- Loudness
- Tempo
- Valence
- Liveness
- Explicit Content
- Duração
- Gênero musical
- Artista

---

## Etapas do Projeto

### 1. Limpeza dos Dados

- Remoção de valores ausentes
- Remoção de duplicatas
- Exclusão de colunas irrelevantes

### 2. Análise Exploratória (EDA)

Foram realizadas análises como:

- Popularidade média por gênero
- Top gêneros mais populares
- Correlação entre variáveis musicais
- Comparação entre músicas explícitas e não explícitas
- Ranking dos artistas mais populares
- Ranking das músicas mais populares

### 3. Engenharia de Features

Criação das variáveis:

- target
- explicit_value

para utilização no modelo de classificação.

### 4. Machine Learning

Modelo utilizado:

Random Forest Classifier

Variáveis de entrada:

- duration_ms
- danceability
- energy
- loudness
- mode
- liveness
- valence
- tempo
- time_signature
- explicit_value

Variável alvo:

- target

### 5. Validação

O desempenho do modelo foi avaliado utilizando:

- Train/Test Split
- Cross Validation (5 folds)
- Classification Report

---

## Tecnologias Utilizadas

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-Learn
- KaggleHub

---

## Resultados

O modelo foi capaz de identificar padrões associados à popularidade musical utilizando características acústicas das músicas.

A validação cruzada foi utilizada para garantir maior robustez dos resultados.

---

## Exemplo de Predição

O usuário pode fornecer características de uma música:

```python
[230666, 0.676, 0.461, -6.746, 1, 0.358, 0.715, 87.917, 4, 0]
