# Tech Challenge — Fase 2 | POSTECH Data Analytics


## 1. Identificação

| Campo | Valor |
|---|---|
| Turma | 2DTATBB |
| Grupo | 09 |
| Data de entrega | 10/10/2026 |

### Integrantes

| Nome completo | RM | E-mail |
|---|---|---|
| Josuelito Balbino da Silva | RM377802 | josuelito.silva@bb.com.br |
| Joyce Kelly Simplicio da Lage | RM377803 | jkslage@hotmail.com |
| Tiago de Almeida Silva | RM377768 | tiago.silva.330@bb.com.br |
| | | |


---

## 2. Links da entrega

Estes três links são **obrigatórios** e devem ser idênticos aos do PDF de submissão.

| Item | Link |
|---|---|
| Repositório | https://github.com/tiago-deas/postech-tech-challenge-fase2.git |
| Vídeo executivo (≤ 5 min) | <!-- PREENCHER: YouTube não listado / Drive com acesso liberado --> |
| Apresentação | https://github.com/tiago-deas/postech-tech-challenge-fase2/blob/main/docs/apresentacao_executiva.pdf |

> ⚠️ Repositório privado ou inacessível inviabiliza a avaliação da entrega.
> Confira o acesso em uma janela anônima antes de enviar.

---

## 3. O problema

O objetivo do projeto é utilizar Machine Learning para classificar solicitantes de cartão de crédito em "bons" ou "maus" pagadores a partir de seu perfil socioeconômico. A motivação de negócio é automatizar a análise de crédito e identificar padrões históricos para mitigar a inadimplência e tomar decisões de concessão mais ágeis e precisas.

### Variável alvo

A variável alvo (TARGET) foi definida a partir da coluna STATUS da base de histórico de pagamentos (credit_record.csv), sendo binarizada para classificar o cliente como 0 (Bom Pagador), caso tenha mantido seus pagamentos em dia ou com atraso máximo de 29 dias (STATUS C, X ou 0), ou 1 (Mau Pagador), caso tenha registrado atraso igual ou superior a 30 dias (STATUS de 1 a 5) em qualquer mês do período observado. O limiar de 30 dias foi adotado por ser a métrica padrão no mercado financeiro para sinalizar o início da inadimplência e o risco de crédito, resultando em uma base fortemente desbalanceada. Foi utilizado a janela de 12 meses para os clientes.

### Dataset

| Campo | Valor |
|---|---|
| Fonte | https://www.kaggle.com/datasets/rikdifos/credit-card-approval-prediction/data |
| Linhas × colunas | application_record.csv = 438.557 x 18 |
| Linhas × colunas | credit_record.csv = 1.048.575 x 3 |
| Período / versão | Versão 2 (Version 2), disponibilizada publicamente pelo utilizador rikdifos em 2020. |
| Licença de uso | CC0: Public Domain |

Descrição das variáveis:

### 1. `application_record.csv`

| Variável | Tipo | Descrição |
|---|---|---|
| `ID` | int64 | Identificador único do cliente / proposta |
| `CODE_GENDER` | object | Gênero do cliente (M = Masculino, F = Feminino) |
| `FLAG_OWN_CAR` | object | Indica se possui veículo próprio (Y = Sim, N = Não) |
| `FLAG_OWN_REALTY` | object | Indica se possui imóvel próprio (Y = Sim, N = Não) |
| `CNT_CHILDREN` | int64 | Quantidade de filhos |
| `AMT_INCOME_TOTAL` | float64 | Renda anual total |
| `NAME_INCOME_TYPE` | object | Categoria do tipo de renda (ex.: Working, Commercial associate, Pensioner, State servant, Student) |
| `NAME_EDUCATION_TYPE` | object | Nível de escolaridade (ex.: Higher education, Secondary / secondary special, etc.) |
| `NAME_FAMILY_STATUS` | object | Estado civil (ex.: Married, Single / not married, Civil marriage, Separated, Widow) |
| `NAME_HOUSING_TYPE` | object | Tipo de moradia (ex.: House / apartment, With parents, Rented apartment, etc.) |
| `DAYS_BIRTH` | int64 | Idade do cliente contada em dias a partir da data atual (valores negativos: -1 = ontem, -365 = 1 ano atrás) |
| `DAYS_EMPLOYED` | int64 | Tempo de emprego contado em dias a partir da data atual (valores negativos; valor positivo 365243 indica pessoa desempregada/aposentada) |
| `FLAG_MOBIL` | int64 | Indica se possui telefone celular (1 = Sim, 0 = Não) |
| `FLAG_WORK_PHONE` | int64 | Indica se possui telefone do trabalho (1 = Sim, 0 = Não) |
| `FLAG_PHONE` | int64 | Indica se possui telefone residencial (1 = Sim, 0 = Não) |
| `FLAG_EMAIL` | int64 | Indica se possui e-mail cadastrado (1 = Sim, 0 = Não) |
| `OCCUPATION_TYPE` | object | Ocupação / profissão do cliente (possui valores nulos) |
| `CNT_FAM_MEMBERS` | float64 | Quantidade total de membros na família |

### 2. `credit_record.csv`

| Variável | Tipo | Descrição |
|---|---|---|
| `ID` | int64 | Identificador único do cliente (chave de ligação com `application_record.csv`) |
| `MONTHS_BALANCE` | int64 | Mês do registro histórico em relação ao mês atual da extração (0 = mês atual, -1 = mês anterior, até -60 = 60 meses atrás) |
| `STATUS` | object | Status do pagamento no mês (C = pago/quitado, X = sem empréstimo, 0 = 1-29 dias de atraso, 1 = 30-59 dias, 2 = 60-89 dias, 3 = 90-119 dias, 4 = 120-149 dias, 5 = atraso > 150 dias ou dívida vencida) |

---

## 4. Como reproduzir

```bash
git clone https://github.com/tiago-deas/postech-tech-challenge-fase2.git
cd postech-tech-challenge-fase2

python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate

pip install -r requirements.txt
jupyter notebook
```

Baixe o dataset e coloque o arquivo bruto em `data/raw/` (os dados **não** são versionados —
veja `data/README.md`).

Depois execute os notebooks nesta ordem:

| # | Notebook | O que faz |
|---|---|---|
| 1 | `notebookstech_challenge.ipynb` | Análise exploratória - Limpeza, escala e feature engineering - Treino e comparação dos modelos, Métricas, importância de variáveis e conclusões |

**Semente fixa:** `RANDOM_STATE = 42`, declarada na primeira célula de cada notebook.
Rodar os notebooks na ordem acima, a partir de um ambiente limpo, deve reproduzir
exatamente os números da seção 5.

---

## 5. Resultados

| Modelo | Acurácia | Precisão | Recall | F1 | AUC-ROC |
|---|---|---|---|---|---|
| Extra Trees | 0.8418 | 0.2314 | 0.4965 | 0.3156 | 0.7426 |
| Random Forest | 0.8415 | 0.2285 | 0.4868 | 0.3110 | 0.7189 |
| Decision Tree | 0.8269 | 0.2197 | 0.5313 | 0.3108 | 0.7025 |
| XGBoost | 0.2704 | 0.0795 | 0.8442 | 0.1453 | 0.5989 |
| Regressão Logística | 0.5559 | 0.0801 | 0.4812 | 0.1374 | 0.5424 |
| Gradient Boosting | 0.9172 | 0.2138 | 0.0473 | 0.0774 | 0.5711 |

**Modelo escolhido:** Random Forest

**Métricas priorizadas:** 

O Random Forest foi selecionado por apresentar a maior média de F1-Score (0,9378) com alto grau de estabilidade e baixo desvio padrão (0,0024) entre todas as dobras da validação cruzada. Isso nos permitiu utilizar o modelo mais adequado para o conjunto de dados que estava desbalanceado. 
    
Resultados da Validação Cruzada

| Modelo | F1-Score (Média) | Desvio Padrão | Scores Individuais |
|---|---|---|---|
| Random Forest | 0.9378 | 0.0024 | [0.9387, 0.9416, 0.9383, 0.9345, 0.9359] |
| Extra Trees | 0.9224 | 0.0023 | [0.9231, 0.9208, 0.9219, 0.9265, 0.9197] |
| XGBoost | 0.8986 | 0.0042 | [0.8979, 0.8914, 0.8987, 0.9039, 0.9014] |

---

## 6. Principais conclusões

Achados de Negócio

1. Janela do Histórico Recente: Considerar o comportamento do cliente em um período recente, em vez do histórico completo, melhora a precisão na reclassificação de risco. Isso evita penalizar clientes que enfrentaram dificuldades no passado distante, mas que hoje mantêm uma boa conduta financeiramente.

2. Maturidade e Tempo de Exposição: Clientes recém-chegados apresentam um risco aparentemente baixo devido à falta de histórico. À medida que o tempo de relacionamento cresce, o comportamento real se revela, exigindo concessões de crédito mais graduais e conservadoras no início.

3. Desbalanceamento e Ajuste do Modelo: A base é predominantemente composta por bons pagadores. Por conta desse forte desequilíbrio, o modelo e as regras de aprovação devem ser calibrados para priorizar a detecção de potenciais inadimplentes, minimizando o custo financeiro associado a aprovações indevidas.

4. Tratamento de Clientes Sem Histórico: A presença de clientes sem movimentação ativa ou histórico observável requer uma abordagem diferenciada. Incluí-los diretamente no modelo analítico gera ruído.

Principais Variáveis e Impacto Prático

1. Tempo de Emprego e Tipo de Ocupação: Refletem a estabilidade da fonte pagadora e a previsibilidade de receita do cliente para honrar seus compromissos.

2. Idade do Cliente: Funciona como um indicador da maturidade do perfil financeiro e da estabilidade comportamental ao longo do tempo.

3. Renda Total Declarada: Define a capacidade financeira e o nível de folga no orçamento para absorver imprevistos sem entrar em atraso.

4. Posse de Bens (Imóvel e Veículo): Serve como um sinal indireto de solvência e saúde patrimonial do tomador de crédito.


### Limitações e próximos passos

Forte desbalanceamento da base onde o grupo de mal pagadores (1) era explicitamente menor do que o de bons pagadores (0).

---

## 7. Estrutura do repositório

```
.
├── data/          dados brutos (raw) e tratados (processed) — não versionados
├── notebooks/     análise em ordem numerada
└── docs/          apresentação executiva
```

Detalhes e convenções em [`ESTRUTURA.md`](ESTRUTURA.md).
Antes de enviar, percorra o [`CHECKLIST.md`](CHECKLIST.md).

---

## 8. Tecnologias

## 8. Tecnologias

| Categoria | Tecnologia / Biblioteca | Versão |
| :--- | :--- | :--- |
| **Linguagem / Runtime** | Python | `3.13` |
| **Manipulação de Dados** | pandas | `2.2.3` |
| | numpy | `2.1.3` |
| **Machine Learning & Stats** | scikit-learn | `1.6.1` |
| | scipy | `1.16.3` |
| | statsmodels | `0.15.0` |
| | imbalanced-learn | `0.14.2` |
| **Modelos de Boosting** | xgboost | `3.4.1` |
| | lightgbm | `4.6.0` |
| **Deep Learning** | torch (PyTorch) | `2.11.0` |
| | tensorflow | `2.21.0` |
| | keras | `3.13.2` |
| **Visualização de Dados** | matplotlib | `3.10.0` |
| | seaborn | `0.13.2` |
| | plotly | `5.24.1` |
| **Explicabilidade de Modelos** | shap | `0.52.0` |
