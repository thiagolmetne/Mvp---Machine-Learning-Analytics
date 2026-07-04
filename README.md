🏅 MVP: Previsão de Performance Olímpica - Machine Learning

📝 Visão Geral

Este projeto aplica técnicas de Machine Learning para prever o sucesso de delegações nos Jogos Olímpicos de Verão. O objetivo central é estimar o número total de medalhas através de variáveis socioeconômicas e do histórico de sedes, utilizando um fluxo de trabalho (pipeline) rigoroso e reprodutível.

🏗️ Arquitetura do Projeto

O projeto foi estruturado para garantir a integridade dos dados e evitar o Data Leakage:

Pré-processamento: Imputação de dados faltantes, transformação logarítmica (log1p) em variáveis de PIB e codificação (OneHotEncoder) de variáveis categóricas.
Pipeline: Todo o fluxo de transformação e modelagem está contido em um Pipeline do Scikit-Learn.
Modelagem: Comparação entre modelo baseline (DummyRegressor), modelo linear (Ridge) e modelo de ensemble (XGBoost).
Otimização: Uso de RandomizedSearchCV com busca em grade para ajuste fino dos hiperparâmetros do XGBoost.

📊 Análise Detalhada dos Resultados

1. Desempenho dos Modelos (Métricas de Erro)
Baseline (DummyRegressor): Estabeleceu a média como previsão. Serviu como comparativo de viés.
Modelo Linear (Ridge): Capturou a tendência geral, mas falhou em capturar a volatilidade de países com alta performance.
XGBoost: O melhor modelo. Sua capacidade de capturar não-linearidades permitiu que o erro (RMSE) caísse significativamente, especialmente para nações que possuem histórico de investimento.

| Modelo | MAE | RMSE | R² |
| --- | --- | --- | --- |
| Dummy | ~12.5 | ~25.0 | < 0 |
| Ridge | ~8.2 | ~15.1 | ~0.65 |
| XGBoost | ~4.8 | ~9.2 | ~0.88 |

2. Análise de Erros e Resíduos
Efeito Sede: O modelo identificou com clareza o host effect. Em edições como BRA (2016) e GBR (2012), o modelo previu um incremento de performance que se alinhou aos dados observados.
Outliers: Países de performance extrema (EUA, China) geram resíduos maiores. O modelo tende a ser conservador, subestimando delegações que possuem superávit de investimento específico no ciclo olímpico.

🚀 Conclusão e Reflexão Crítica

O modelo demonstra uma robustez satisfatória para fins analíticos. A escolha do XGBoost foi justificada pela sua eficácia em tabular dados heterogêneos.

Limitações Atuais:

Discrepância de Contagem: Uma modelagem futura com Poisson Regression seria o passo ideal para dados de contagem.
Variáveis Latentes: O sucesso olímpico depende de "esforço investido" — uma variável difícil de quantificar apenas por PIB.
🛠️ Como Executar

Ambiente: O projeto é totalmente compatível com Google Colab.
Setup:
pip install pandas numpy scikit-learn xgboost joblib

💡 Próximos Passos (Roadmap)

 Feature Engineering: Incluir número de atletas classificados e investimentos por modalidade.
 Explorabilidade (XAI): Implementar SHAP Values para explicar quais variáveis mais pesaram na previsão de cada país.
 Quantile Regression: Estimar não apenas o valor esperado, mas o "intervalo de confiança" das medalhas (ex: entre 5 e 10 medalhas).
 
👤 Contato
Thiago Luiz Metne | Thiagol.metne@gmail.com



