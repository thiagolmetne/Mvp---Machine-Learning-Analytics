MVP: Previsão de Total de Medalhas — Olimpíadas de Verão
Resumo
Projeto MVP (Machine Learning & Analytics) que prevê o total de medalhas por delegação nas Olimpíadas de Verão usando um modelo de regressão. O notebook aplica fluxo reprodutível: definição do problema, EDA, pré-processamento, modelagem, ajuste de hiperparâmetros, avaliação temporal (time‑split) e conclusão.

Dados  

Fonte: CSV fornecido no repositório (ou link público).
Colunas principais: ano, delegacao, nivel_renda, media_gdp, total_medalhas, qtd_paises.
Target: total_medalhas (regressão de contagem).
Observação: consideramos apenas Olimpíadas de Verão e usamos time‑split (treino = todos os anos anteriores; teste = último ano).
Estrutura do repositório

mvp_olimpiadas.ipynb — notebook Colab/Jupyter reprodutível com todo o fluxo.
mvp_olimpiadas_best_model.joblib — (opcional) modelo salvo gerado pelo notebook.
data/ — pasta com o CSV (ou link para download).
README.md — este arquivo.
Como executar (Colab)

Abra o notebook no Colab: File → Upload notebook (ou use "Open in Colab" se hospedado no GitHub).
Se necessário, faça upload do CSV quando o notebook pedir ou defina DATA_URL no topo.
Execute células em ordem. Tempo estimado: minutos para EDA e modelos simples; tuning (RandomizedSearchCV n_iter=10) pode levar de alguns minutos até ~15–30 min dependendo do runtime.
Ao final, baixe o .ipynb ou salve direto no GitHub via File → Save a copy in GitHub.
Dependências principais

Python 3.8+
pandas, numpy, matplotlib, seaborn
scikit-learn
xgboost
joblib
(Instalações sugeridas via pip; o notebook inclui instalação de xgboost se necessário.)
Metodologia (resumo)

Pré‑processamento: imputação (mediana para media_gdp), log1p(media_gdp), imputação de nivel_renda com 'Unknown', codificação top‑N delegações (OUTROS), padronização numérica.
Time‑split: treino com anos < max(ano); teste = registros do último ano (simula previsão para edição mais recente).
Baseline: DummyRegressor (média).
Modelos candidatos: Ridge, RandomForest, XGBoost.
Hiperparâmetros: RandomizedSearchCV (n_iter=10) aplicado ao XGBoost.
Métricas: MAE, RMSE, R²; plots de predito vs real; importância de features.
Resultados (preencha após executar)

Melhor modelo:
MAE (teste):
RMSE (teste):
R² (teste):
Observações:

Enriquecimento de features: adicionar nº de atletas, investimento esportivo, população, PIB per capita e histórico por esporte.
Granularidade por esporte: prever medalhas por delegação×esporte e agregar para capturar heterogeneidade.
Modelos de contagem: usar Poisson / Negative Binomial / zero‑inflated para tratar zeros e overdispersion.
Codificação avançada de países: target encoding temporalmente seguro, embeddings ou agrupamento por região.
Validação temporal robusta: rolling/expanding time‑splits para avaliar generalização ao longo dos anos.
Otimização e ensembles: busca bayesiana (Optuna) e stacking/ensembles para melhorar desempenho.
Incerteza e previsões probabilísticas: quantile regression, conformal prediction ou modelos bayesianos para intervalos de confiança.
Explainability e análise de erros: SHAP/PDPs e análise de resíduos por país/região para interpretar e diagnosticar o modelo.

Contato
Thiago Luiz Metne / Thiagol.metne@gmail.com
