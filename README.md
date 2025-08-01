#  Previsão de Evasão de Clientes - Telecom X

##  Descrição do Projeto

Este projeto tem como objetivo prever a evasão (churn) de clientes da empresa Telecom X com base em dados históricos. A previsão permite à empresa identificar os fatores que mais influenciam a saída de clientes e implementar estratégias eficazes de retenção.

---

##  Fonte dos Dados

Os dados foram carregados a partir de um arquivo `.csv`, contendo variáveis demográficas, contratuais, de serviços utilizados, forma de pagamento e valores cobrados.
A variável-alvo é `Evasao`, onde:

* `1` = cliente evadiu (churn)
* `0` = cliente ativo

---

##  Bibliotecas Utilizadas

* **Pandas** – Manipulação e análise de dados (`read_csv`, `DataFrame`, etc.)
* **NumPy** – Operações matemáticas e vetorizacão
* **Matplotlib** e **Seaborn** – Visualização de dados (gráficos, histogramas, etc.)
* **Scikit-learn (sklearn)** – Modelagem, métricas, pré-processamento:

  * `train_test_split`, `StandardScaler`, `LogisticRegression`, `RandomForestClassifier`, `confusion_matrix`, `classification_report`, etc.
* **Imbalanced-learn (imblearn)** – Balanceamento de classes com **SMOTE**
* **Joblib** – Salvamento e carregamento dos modelos treinados

---

## ⚙ Etapas do Projeto

### 1.  Leitura e Preparação dos Dados

* Leitura do arquivo CSV com `pandas`.
* Verificação e tratamento de valores ausentes.
* Conversão de tipos de dados.
* Renomeação de colunas para facilitar a análise.

### 2.  Pré-processamento

* One-Hot Encoding das variáveis categóricas.
* Normalização das variáveis numéricas com `StandardScaler`.
* Separar `X` (variáveis preditoras) e `y` (variável-alvo).
* Divisão dos dados em treino/teste com estratificação (80% / 20%).
* Aplicação de **SMOTE** para balanceamento das classes no treino.

### 3.  Modelagem Preditiva

####  Regressão Logística

Modelo linear treinado com dados padronizados. Serviu como baseline para comparação.

####  Random Forest

Modelo de ensemble robusto, treinado sem necessidade de normalização. Útil para extração de importância de variáveis.

### 4.  Avaliação dos Modelos

Métricas utilizadas:

* Acurácia
* Precisão
* Recall
* F1-score
* Matriz de Confusão

---

##  Análise de Importância das Variáveis

###  Random Forest – Top 5 variáveis

| Variável                          | Importância |
| --------------------------------- | ----------- |
| Custo\_Total                      | 0.117       |
| Tempo\_de\_Contrato               | 0.108       |
| Custo\_Mensal                     | 0.099       |
| Tipo\_de\_Contrato\_Mensal        | 0.094       |
| Metodo\_de\_Pagamento\_Electronic | 0.079       |

###  Regressão Logística – Top 5 coeficientes (valores absolutos)

| Variável                   | Coeficiente | Importância Absoluta |
| -------------------------- | ----------- | -------------------- |
| Tempo\_de\_Contrato        | -1.486      | 1.486                |
| Custo\_Mensal              | -1.026      | 1.026                |
| Custo\_Total               | 0.807       | 0.807                |
| Tipo\_de\_Contrato\_Mensal | 0.271       | 0.271                |
| Faturamento\_Sem\_Papel    | 0.187       | 0.187                |

---

##  Conclusões

* **Tempo de contrato curto**, **pagamento eletrônico**, **contrato mensal** e **faturamento digital** aumentam as chances de evasão.
* O **Random Forest** teve melhor desempenho geral, enquanto a **Regressão Logística** mostrou boa interpretabilidade dos fatores.
* Serviços como **fibra óptica**, **suporte técnico** e **streaming** também influenciam na permanência do cliente.

---

##  Estratégias Recomendadas

1. **Incentivar contratos longos** com ofertas personalizadas.
2. **Reduzir atritos** no pagamento eletrônico com melhorias na experiência.
3. **Engajar novos clientes** nos primeiros meses com suporte proativo.
4. **Oferecer pacotes combinados** com serviços adicionais.

---

##  Salvamento e Reutilização dos Modelos

Os modelos foram salvos utilizando a biblioteca `joblib`:

```python
from joblib import dump, load

# Exemplo de salvamento
dump(modelo_rf, 'modelo_random_forest.joblib')
dump(modelo_lr, 'modelo_regressao_logistica.joblib')
```

Eles podem ser carregados posteriormente com:

```python
modelo = load('modelo_random_forest.joblib')
```

---

Pronto para publicação no GitHub ✔️
