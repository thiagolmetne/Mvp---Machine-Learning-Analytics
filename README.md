# MVP: Previsão de Total de Medalhas — Olimpíadas de Verão

## 📋 Resumo

Projeto MVP (Machine Learning & Analytics) que prevê o total de medalhas por delegação nas Olimpíadas de Verão usando um modelo de regressão. O notebook aplica um **fluxo reprodutível completo**: desde análise exploratória até tuning de hiperparâmetros e salvamento do modelo.

**Objetivo:** Comparar modelos de regressão (Dummy, Ridge, Random Forest, XGBoost) e identificar o melhor desempenho usando validação temporal.

---

## 📊 Dados

- **Fonte:** CSV fornecido no repositório (`gpd_medalha-000000000000.csv`)
- **Colunas principais:** 
  - `ano`, `delegacao`, `nivel_renda`, `media_gdp`, `total_medalhas`, `qtd_paises`
- **Target:** `total_medalhas` (regressão de contagem)
- **Escopo:** Apenas Olimpíadas de Verão
- **Validação:** Time-split temporal (treino = anos anteriores; teste = último ano)

---

## 📁 Estrutura do Repositório

```
.
├── MVP_Analise_de_Medalhas_por_GPD.ipynb    # Notebook principal (Jupyter/Colab)
├── mvp_olimpiadas_best_model.joblib         # Modelo treinado (gerado ao executar)
├── gpd_medalha-000000000000.csv             # Dataset
├── README.md                                  # Este arquivo
└── data/                                      # (opcional) Pasta com CSVs adicionais
```

---

## 🚀 Como Executar (Colab)

### Passo 1: Abrir o Notebook
1. Acesse [Google Colab](https://colab.research.google.com/)
2. Faça upload do `.ipynb` ou clique em **File → Open notebook** e selecione de GitHub
3. Ou acesse diretamente: 
   - Copie a URL do notebook do GitHub
   - Coloque em: `https://colab.research.google.com/github/thiagolmetne/Mvp---Machine-Learning-Analytics/blob/main/MVP_Analise_de_Medalhas_por_GPD.ipynb`

### Passo 2: Configurar Dados
- Se necessário, ajuste `DATA_URL` no topo da célula 2 para apontar para seu CSV
- Ou deixe em branco para fazer upload manual quando o notebook pedir

### Passo 3: Executar Células
- Execute as células **em ordem** (Ctrl+Enter ou Shift+Enter)
- **Tempo estimado:**
  - EDA + Modelos Base: ~2-3 minutos
  - Tuning XGBoost: ~5-10 minutos (depende do runtime)
  - Total: ~10-15 minutos

### Passo 4: Salvar Resultados
- O modelo será salvo como `mvp_olimpiadas_best_model.joblib`
- Baixe via **Files** (painel esquerdo) ou salve no GitHub com **File → Save a copy in GitHub**

---

## 📦 Dependências Principais

```
Python 3.8+
pandas >= 1.0.0
numpy >= 1.19.0
matplotlib >= 3.2.0
seaborn >= 0.11.0
scikit-learn >= 0.24.0
xgboost >= 1.3.0
joblib >= 1.0.0
scipy >= 1.5.0
```

**Instalação (automática no notebook):**
```bash
pip install pandas numpy matplotlib seaborn scikit-learn xgboost joblib scipy
```

---

## 🔬 Metodologia

### 1. Pré-processamento
- ✓ Imputação: mediana para `media_gdp`, mode/constant para categóricas
- ✓ Transformação: `log1p(media_gdp)` para lidar com assimetria
- ✓ Codificação: one-hot encoding com top-N delegações (OUTROS para resto)
- ✓ Padronização: StandardScaler para features numéricas

### 2. Validação Temporal
- **Treino:** Todos os anos < ano_máximo
- **Teste:** Registros do último ano
- **Justificativa:** Simula cenário realista de previsão para nova edição

### 3. Modelos Candidatos
| Modelo | Propósito | Hiperparâmetros |
|--------|----------|-----------------|
| **Dummy** | Baseline (média) | N/A |
| **Ridge** | Regressão linear regularizada | α=1.0 |
| **Random Forest** | Ensemble não-paramétrico | n_estimators=100, max_depth=15 |
| **XGBoost** | Gradient boosting | n_estimators=100, max_depth=6, learning_rate=0.1 |
| **XGBoost Tuned** | XGB com RandomizedSearchCV | 20 iterações, 3-fold CV |

### 4. Métricas de Avaliação
- **MAE (Mean Absolute Error):** Erro médio absoluto
- **RMSE (Root Mean Squared Error):** Raiz do erro quadrático médio
- **R² Score:** Coeficiente de determinação (0 a 1, maior é melhor)
- **CV MAE:** Validação cruzada (k-fold=3 ou 4)

### 5. Tuning de Hiperparâmetros
- **Método:** RandomizedSearchCV (20 iterações)
- **Scoring:** `neg_mean_absolute_error`
- **CV:** KFold (3 splits, shuffle=True)
- **Grid de Parâmetros:**
  ```python
  n_estimators: [50, 300]
  max_depth: [3, 10]
  learning_rate: [0.01, 0.31]
  subsample: [0.6, 1.0]
  colsample_bytree: [0.5, 1.0]
  min_child_weight: [1, 5]
  ```

---

## 📈 Resultados (Preencher após Execução)

### Comparação Final de Modelos
| Modelo | Train MAE | Test MAE | Test RMSE | Test R² |
|--------|-----------|----------|-----------|---------|
| Dummy | - | - | - | - |
| Ridge | - | - | - | - |
| Random Forest | - | - | - | - |
| XGBoost | - | - | - | - |
| **XGBoost Tuned** | - | - | - | - |

### Melhor Modelo
- **Nome:** `[PREENCHIDO]`
- **Test MAE:** `[PREENCHIDO]`
- **Test RMSE:** `[PREENCHIDO]`
- **Test R²:** `[PREENCHIDO]`

### Feature Importance (Top 5)
1. `[PREENCHIDO]`
2. `[PREENCHIDO]`
3. `[PREENCHIDO]`
4. `[PREENCHIDO]`
5. `[PREENCHIDO]`

---

## 🔍 Interpretação dos Resultados

### Métricas
- **MAE:** Erro médio em número de medalhas (unidade original)
- **RMSE:** Penaliza erros grandes mais que MAE
- **R²:** % da variância explicada (ex: R²=0.85 → 85% da variância explicada)

### Bom Desempenho
- ✓ Test R² > 0.7
- ✓ Test MAE próximo ao baseline (Dummy) significaria overfitting
- ✓ Test MAE < Train MAE descarta overfitting
- ✓ CV MAE < Test MAE confirma generalização

---

## 🚨 Limitações Atuais

1. **Features Limitadas**
   - Apenas GDP, renda, ano, nº de países
   - Faltam: investimento esportivo, população, PIB per capita, histórico de performance

2. **Agregação por Delegação**
   - Perda de granularidade por esporte (futebol, natação, etc.)
   - Dinâmicas diferentes em cada esporte

3. **Ausência de Features Históricas**
   - Sem medalhas em Olimpíadas passadas
   - Sem evolução temporal capturada

4. **Distribuição de Dados**
   - Possível zero-inflação (muitas delegações com 0 medalhas)
   - Regressão linear pode não ser ideal para dados de contagem

---

## 💡 Próximos Passos Recomendados

### Curto Prazo (Fácil)
1. **Enriquecimento de Features**
   - Adicionar histórico: medalhas nos últimos 2-3 ciclos olímpicos
   - Features de região geográfica
   - Log(população), Log(PIB per capita)

2. **Validação Temporal Robusta**
   - Implementar rolling time-splits (ex: treino em 2-3 ciclos, teste no próximo)
   - Expanding window validation

### Médio Prazo (Moderado)
3. **Modelos de Contagem**
   - Poisson Regression
   - Negative Binomial Regression
   - Zero-Inflated Poisson (ZIP)

4. **Ensembles e Stacking**
   - Combinar Ridge + RF + XGB com meta-learner
   - Busca Bayesiana (Optuna) em vez de RandomizedSearchCV

### Longo Prazo (Avançado)
5. **Granularidade por Esporte**
   - Prever medalhas por delegação × esporte
   - Agregar para capturar heterogeneidade entre esportes

6. **Incerteza e Intervalos**
   - Quantile Regression (predições percentis, ex: 5%, 50%, 95%)
   - Conformal Prediction (garantir cobertura nominal)
   - Modelos Bayesianos (distribuições posteriores)

7. **Explainability**
   - SHAP (SHapley Additive exPlanations)
   - Partial Dependence Plots (PDPs)
   - Análise de resíduos por país/região/renda

---

## 📝 Notas Importantes

### Reprodutibilidade
- `RANDOM_STATE = 42` garante resultados consistentes
- Sempre execute as células em ordem sequencial
- Não reinicie o kernel entre execuções

### Tempo de Execução
- **Sem tuning:** ~2-3 minutos
- **Com tuning (20 iter, 3-fold CV):** ~5-10 minutos
- **Em GPU Colab:** ~2-3 minutos (com tuning)

### Dicas de Otimização
- ✓ Usar Google Colab com GPU (Conectar → Alterar tipo de runtime → GPU)
- ✓ Reduzir `n_iter` em `RandomizedSearchCV` se demorar muito
- ✓ Aumentar `TOP_N_DELEGACOES` para capturar mais países

---

## 👤 Autor

**Thiago Luiz Metne**
- 📧 Email: thiagol.metne@gmail.com
- 🔗 GitHub: [@thiagolmetne](https://github.com/thiagolmetne)

---

## 📄 Licença

Este projeto é fornecido como está. Sinta-se livre para usar, modificar e distribuir conforme necessário.

---

## 🤝 Contribuições

Sugestões e melhorias são bem-vindas! Abra uma **issue** ou **pull request** com suas ideias.

---

**Última atualização:** 2024
