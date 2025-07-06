# Sumarização Abstrata de Diálogos com Redes LSTM e Mecanismo de Atenção

Este repositório apresenta o desenvolvimento de um sistema de **sumarização automática de diálogos** utilizando técnicas de **Processamento de Linguagem Natural (PLN)** e **Deep Learning**, com foco em redes LSTM combinadas com **atenção aditiva (Additive Attention)**.

---

## 📌 Proposta do Projeto

O objetivo deste projeto é construir um modelo capaz de gerar **resumos abstratos** de diálogos escritos, sintetizando o conteúdo principal em poucas palavras. A ideia central é resolver um desafio clássico de PLN: **reduzir um texto extenso (diálogo) a uma forma mais concisa (resumo)**, sem apenas extrair frases, mas **gerando novos enunciados semanticamente equivalentes**.

Essa tarefa é essencial em aplicações como:
- Assistentes virtuais (resumo de conversas),
- Atendimento automatizado ao cliente,
- Educação e correção de redações,
- Compressão de conteúdo para acessibilidade.

---

## 🧪 Tecnologias Utilizadas

- **Linguagem**: Python 3
- **Bibliotecas principais**:  
  `TensorFlow`, `Keras`, `NLTK`, `Pandas`, `Matplotlib`, `Seaborn`, `ROUGE`, `BLEU`, `Textstat`, `WordCloud`, `Contractions`
- **Ambiente**: Google Colab com conexão ao Google Drive

---

## 🧱 Etapas do Pipeline

### 1. Preparação do ambiente
Instalação das bibliotecas necessárias e montagem do Google Drive para leitura dos arquivos `.csv`.

### 2. Carregamento dos dados
Os dados utilizados estão divididos em três arquivos:
- `dialogo-train.csv`
- `dialogo-validation.csv`
- `dialogo-test.csv`

Cada entrada contém:
- `id`
- `dialogue`: texto com o diálogo completo
- `summary`: resumo manual associado
- `split`: flag indicando o conjunto de origem (train, val, test)

---

### 3. Análise Exploratória de Dados (EDA)
Exploração visual e estatística de:
- Distribuição dos comprimentos de diálogos e resumos
- Índices de legibilidade (Flesch Reading Ease)
- Similaridade entre diálogo e resumo (Jaccard)
- Taxa de compressão textual
- Grau de novidade (novelty ratio) nos resumos

Essas análises revelam a complexidade e a variedade dos dados, justificando a abordagem com redes neurais e atenção.

---

### 4. Pré-processamento
O pipeline de limpeza textual incluiu:
- Conversão para minúsculas
- Remoção de HTML, URLs, emojis e caracteres especiais
- Expansão de contrações e gírias de chat
- Normalização de espaços e pontuação

Esse processo garante um vocabulário mais limpo e uniforme para o modelo.

---

### 5. Modelagem: LSTM + Atenção

#### Arquitetura:
- **Encoder**: LSTM bidirecional que processa os diálogos
- **Decoder**: LSTM com mecanismo de atenção que gera resumos
- **Atenção aditiva (Bahdanau)**: ajuda o modelo a focar em partes relevantes do diálogo durante a geração do resumo
- **Tokenização**: baseada em `Tokenizer` do Keras com padding
- **Objetivo**: prever o próximo token do resumo, dado o diálogo e os tokens anteriores

#### Treinamento:
- Otimizador: `Adam`
- Função de perda: `sparse_categorical_crossentropy`
- Callbacks: `EarlyStopping`, `ModelCheckpoint`, `ReduceLROnPlateau`, `TensorBoard`

---

### 6. Avaliação do Modelo

Foram utilizadas métricas padrão para tarefas de geração de texto:

- **BLEU Score**: 0.9805  
  Avalia a precisão n-gram entre resumos reais e previstos.

- **ROUGE Scores**:
  - ROUGE-1: 0.9917
  - ROUGE-2: 0.9842
  - ROUGE-L: 0.9917  
  Avaliam a sobreposição entre as sequências reais e geradas.

---
## Resultados
Os arquivos CSV completos e resultados de predições estão disponíveis no link abaixo:

🔗 Acesse os dados e resultados no Google Drive
(Contém os arquivos: Dados e Resultados
Os arquivos CSV e resultados de predições estão disponíveis no link abaixo:

🔗 Acesse os dados e resultados no Google Drive
(Contém os arquivos: https://drive.google.com/drive/folders/1bax143ZqwO6fKguDbVWHL7tRFw9uO3A_?usp=sharing)
