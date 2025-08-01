# Projeto de Previsão de Evasão de Clientes – Telecom X

##  Objetivo
Desenvolver um modelo preditivo capaz de identificar clientes com maior propensão à evasão (churn) com base em dados comportamentais, demográficos e de serviços da empresa **Telecom X**. A intenção é apoiar estratégias de retenção e melhorar a experiência do cliente.

##  Estrutura do Projeto

### 1. Entendimento e Leitura dos Dados
- Leitura do arquivo 
- Expansão de colunas aninhadas como `customer`, `internet`, `charges`, entre outras
- Criação do DataFrame final com colunas tabulares

### 2. 🔍 Tratamento e Preparação dos Dados
- Padronização de valores como `"No internet service"` e `"No phone service"` para `"No"`
- Conversão de variáveis categóricas para formato apropriado
- Conversão de variáveis numéricas (ex: `Charges.Total`) de `object` para `float`
- Tratamento de valores ausentes

### 3. 🧼 Engenharia de Atributos
- Renomeação de colunas para nomes mais curtos e intuitivos
- Transformações como criação de dummies (One-Hot Encoding)
- Normalização (apenas para modelos sensíveis à escala, como Regressão Logística)

### 4. ⚖️ Balanceamento de Classes
- Aplicação de **SMOTE** no conjunto de treino para equilibrar as classes (`Churn: 0 / 1`)

### 5. 🤖 Modelagem
Treinamento e avaliação de dois algoritmos:

#### ✅ Regressão Logística
- Padronização dos dados
- Avaliação com métricas: Acurácia, Precisão, Recall, F1-score

#### 🌳 Random Forest
- Sem necessidade de padronização
- Avaliação com as mesmas métricas

### 6. 📉 Avaliação de Desempenho
Comparação entre os dois modelos com base nas métricas:

| Modelo               | Acurácia | Precisão | Recall | F1-score |
|----------------------|----------|----------|--------|----------|
| Regressão Logística  | Ex: 0.79 | ...      | ...    | ...      |
| Random Forest        | Ex: 0.84 | ...      | ...    | ...      |

### 7. 🔎 Análise de Importância das Variáveis

#### 🌳 Random Forest – Top 10 Variáveis:
- `Custo_Total`, `Tempo_de_Contrato`, `Custo_Mensal`, `Tipo_de_Contrato_Mensal`, `Pagamento_Electronic check`, etc.

#### 📈 Regressão Logística – Top 10 por Coeficiente:
- `Tempo_de_Contrato`, `Custo_Mensal`, `Custo_Total`, `Internet_Fiber optic`, `Streaming_TV`, etc.

## 📌 Conclusões

### Principais fatores associados à evasão:
- **Baixo tempo de contrato**
- **Pagamentos via Electronic Check**
- **Internet via Fiber Optic**
- **Contratos Mensais**
- **Faturamento sem papel**

### Estratégias recomendadas:
- Incentivar **contratos mais longos**
- Melhorar **experiência inicial**
- Otimizar **atendimento técnico**
- Estimular **pagamento automático**

## 💾 Reutilização dos Modelos
Modelo Random Forest salvo com `joblib`:

```python
from joblib import dump, load
dump(modelo_random_forest, 'modelo_random_forest.joblib')

 Previsão de Evasão de Clientes - Telecom X

Descrição do Projeto
Este projeto tem como objetivo prever a evasão (churn) de clientes da empresa Telecom X com base em dados históricos. A previsão permite à empresa identificar os fatores que mais influenciam a saída de clientes e implementar estratégias eficazes de retenção.

Estrutura dos Dados
O conjunto de dados foi carregado a partir de um arquivo .csv, contendo variáveis demográficas, contratuais, de serviços utilizados, forma de pagamento e valores cobrados. A variável-alvo é Evasao, com 1 indicando cliente evadido e 0, cliente ativo.

⚙ Etapas do Projeto
1.  Leitura e Preparação dos Dados
Leitura do arquivo CSV com pandas.

Verificação e tratamento de valores ausentes.

Conversão de tipos de dados, especialmente para colunas numéricas e categóricas.

Transformação de colunas aninhadas (quando aplicável).

Renomeação de colunas para facilitar a análise.

2.  Pré-processamento
Codificação de variáveis categóricas com One-Hot Encoding.

Normalização dos dados para modelos sensíveis à escala (como regressão logística).

Separação entre variáveis independentes (X) e variável dependente (y).

Divisão dos dados em treino e teste (80% / 20%) com estratificação.

Aplicação do SMOTE no conjunto de treino para balancear as classes.

3.  Modelagem Preditiva
Foram treinados dois modelos distintos:

 Regressão Logística (com normalização)
Modelo linear utilizado como baseline para avaliação de performance.

 Random Forest (sem necessidade de normalização)
Modelo baseado em árvores de decisão, útil para capturar relações complexas entre as variáveis.

4.  Avaliação dos Modelos
As métricas utilizadas foram:

Acurácia

Precisão

Recall

F1-score

Matriz de Confusão

Comparou-se o desempenho dos dois modelos em termos de balanceamento entre as classes e capacidade de generalização.

 Análise de Importância das Variáveis
 Random Forest
As variáveis mais importantes para o modelo foram:

Variável	Importância
Custo_Total	0.117
Tempo_de_Contrato	0.108
Custo_Mensal	0.099
Tipo_de_Contrato_Mensal	0.094
Metodo_de_Pagamento_Electronic	0.079

 Regressão Logística
A magnitude dos coeficientes indica a influência das variáveis:

Variável	Coeficiente	Importância Absoluta
Tempo_de_Contrato	-1.486	1.486
Custo_Mensal	-1.025	1.026
Custo_Total	0.807	0.807
Tipo_de_Contrato_Mensal	0.271	0.271
Faturamento_Sem_Papel	0.187	0.187

 Conclusões
Clientes com contrato mensal, pagamento eletrônico e menor tempo de contrato apresentam maior propensão à evasão.

O modelo de Random Forest apresentou maior acurácia geral, mas a Regressão Logística teve melhor desempenho na classificação da classe minoritária (clientes evadidos).

O faturamento elevado e uso de serviços como fibra óptica e suporte técnico também influenciam na decisão do cliente permanecer ou sair.

 Estratégias Recomendadas
Oferecer incentivos para migração de contratos mensais para contratos de maior duração.

Melhorar a experiência dos clientes que utilizam pagamento eletrônico.

Monitorar os primeiros meses de relacionamento, pois muitos cancelamentos ocorrem nesse período.

Investir em serviços adicionais, como suporte técnico e segurança online, que demonstraram correlação negativa com a evasão.

Salvamento dos Modelos
Os modelos foram salvos com a biblioteca joblib e podem ser reutilizados para futuras previsões sem a necessidade de reprocessar todo o pipeline.


