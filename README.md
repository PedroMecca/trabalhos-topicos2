# Trabalho 1 — Corpus de Críticas de Filmes (Rotten Tomatoes)

Projeto da disciplina de Processamento de Linguagem Natural (PLN), que consiste em construir, pré-processar e analisar um corpus textual usando técnicas tradicionais de PLN. O resultado serve de base para o **Trabalho 2** (sistema de recomendação de filmes).

## Objetivo

A partir de críticas de filmes do Rotten Tomatoes, o projeto tem dois objetivos:

1. **Classificação de sentimento** — prever se uma crítica é positiva (*Fresh*) ou negativa (*Rotten*) a partir do texto.
2. **Perfil de gêneros favoritos** — identificar, a partir das críticas positivas, quais gêneros um crítico tende a avaliar melhor.

## Dataset de origem

[Rotten Tomatoes Movies and Critic Reviews Dataset](https://www.kaggle.com/datasets/stefanoleone992/rotten-tomatoes-movies-and-critic-reviews-dataset) (Kaggle), usado apenas como matéria-prima. O corpus efetivamente utilizado é construído no notebook a partir da junção, limpeza, deduplicação e amostragem balanceada desses dados brutos.

## Estrutura do repositório

```
├── notebooks/
│   └── Trabalho1_Corpus_RottenTomatoes.ipynb   # notebook completo (Google Colab)
├── CorpusRottenTomatoes/
│   ├── dados_processados/                      # corpus construído e processado
│   │   ├── corpus_reviews.csv
│   │   └── corpus_reviews_processado.csv
│   ├── metadados/                              # metadados do corpus (ids, hashes, contagens)
│   │   ├── metadados_corpus.csv
│   │   └── metadados_corpus.json
│   └── resultados/                             # métricas, gráficos e previsões geradas
│       ├── 01_distribuicao_classes.png
│       ├── 02_generos_frequentes.png
│       ├── 03_matriz_confusao.png
│       ├── 04_comparacao_baseline.png
│       ├── 05_perfil_generos_critico.png
│       ├── metricas.json
│       └── previsoes_teste.csv
├── Relatorio_Tecnico_Trabalho1.docx
└── README.md
```

> A pasta `dados_brutos/` (CSVs originais do Kaggle) não é versionada aqui por serem arquivos grandes e de terceiros — pode ser reconstruída rodando as primeiras células do notebook.

## Pipeline

1. **Coleta** dos dados brutos via API do Kaggle.
2. **Construção do corpus**: junção das tabelas de filmes e críticas, limpeza, remoção de duplicatas (hash) e amostragem balanceada.
3. **Pré-processamento**: limpeza de texto, tokenização (NLTK), remoção de stopwords, lematização (spaCy) e representação por TF-IDF.
4. **Análise**: classificação de sentimento com Regressão Logística; análise complementar de perfil de gêneros por crítico.
5. **Avaliação**: acurácia, precisão, revocação, F1, matriz de confusão, análise de erros e comparação com baseline (classificador de maioria).

## Como executar

O notebook foi feito para rodar no **Google Colab**. Basta abrir `notebooks/Trabalho1_Corpus_RottenTomatoes.ipynb`, executar as células em ordem e informar suas próprias credenciais da API do Kaggle quando solicitado (não são incluídas neste repositório).

## Resultados (resumo)

| Modelo | Acurácia | F1 (ponderado) |
|---|---|---|
| Baseline (classe majoritária) | ~0,51 | ~0,35 |
| Regressão Logística + TF-IDF | ~0,87 | ~0,87 |

Detalhes completos, discussão de vieses/limitações e conclusões estão no relatório técnico (`Relatorio_Tecnico_Trabalho1.docx`).

## Aplicação no Trabalho 2

O corpus, o pipeline de pré-processamento e o perfil de gêneros por crítico construídos aqui servem de base para um sistema de recomendação de filmes: usando o histórico de avaliações de um usuário, é possível sugerir filmes de gêneros historicamente bem avaliados por ele.

## Autor

Pedro Bonelli
