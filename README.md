# Análise de Churn da Telecom X

Este repositório contém um pipeline completo de Extração, Transformação, Carga (ETL) e Análise de Dados para investigar o churn (cancelamento de clientes) na empresa fictícia de telecomunicações "Telecom X". O objetivo principal é identificar os fatores que contribuem para a evasão de clientes e fornecer insights acionáveis para a criação de estratégias de retenção.

O projeto é desenvolvido em um Jupyter Notebook (`TelecomX_BR.ipynb`) e está estruturado em quatro etapas principais: extração, transformação, análise e geração de relatório.

## 🎯 Objetivo do Projeto

  * **Problema:** Um alto índice de cancelamentos (churn) está impactando negativamente a receita e o crescimento da empresa.
  * **Objetivo:** Analisar o comportamento de churn dos clientes para entender suas principais causas.
  * **Meta:** Identificar padrões e fatores-chave que levam à evasão, permitindo o desenvolvimento de estratégias de retenção eficazes.

## ⚙️ Pipeline de Processamento de Dados

O notebook segue um fluxo estruturado para garantir a qualidade e a relevância da análise.

### 1\. Extração (Extraction)

  * Os dados são extraídos de uma fonte JSON hospedada no GitHub através de uma requisição HTTP.
  * A função `extract_telecom_data_github()` gerencia a conexão e carrega os dados brutos em um DataFrame do Pandas.

### 2\. Transformação (Transformation)

Uma série de funções é aplicada para limpar, padronizar e enriquecer os dados. A pipeline de transformação (`run_transformation_pipeline`) inclui:

  * **Tratamento de Valores Ausentes:**
      * Preenchimento de dados faltantes em colunas categóricas (`gender`, `InternetService`).
      * Tratamento inteligente de valores nulos na coluna `TotalCharges`, considerando novos clientes (baixo `tenure`) e preenchendo os demais com a mediana.
  * **Remoção de Duplicatas:** Eliminação de registros totalmente duplicados e de clientes com múltiplos registros, mantendo aquele com informações mais completas.
  * **Padronização de Dados Categóricos:** Correção de inconsistências em colunas como `gender`, `Partner`, `Dependents` e `Churn` (ex: 'M' para 'Male', '1' para 'Yes').
  * **Engenharia de Features:** Criação da nova coluna `Contas_Diarias` para permitir análises mais granulares sobre os gastos dos clientes.
  * **Transformação de Colunas Binárias:** Conversão de colunas com respostas 'Yes'/'No' para o formato numérico (1/0) para facilitar análises quantitativas.
  * **Padronização de Tipos:** Ajuste dos tipos de dados para numéricos e categóricos, garantindo a consistência para as análises.

### 3\. Análise Exploratória (Analysis)

Após o tratamento, os dados são analisados para extrair informações relevantes. A pipeline de análise (`run_analysis_pipeline`) realiza:

  * **Estatísticas Descritivas:** Resumo das principais métricas para variáveis numéricas e categóricas.
  * **Análise de Churn:**
      * Cálculo da distribuição e da taxa geral de churn.
      * Análise cruzada entre variáveis categóricas (ex: tipo de contrato, método de pagamento) e a variável alvo (`Churn`).
      * Comparação de médias e medianas de variáveis numéricas (ex: `tenure`, `MonthlyCharges`) entre clientes que cancelaram e os que permaneceram.
  * **Matriz de Correlação:** Análise da correlação entre as variáveis numéricas para identificar relações lineares.

## 📊 Principais Insights

A análise revelou os seguintes padrões de comportamento:

  * **Taxa Geral de Churn:** Aproximadamente **26.5%** dos clientes na base de dados cancelaram o serviço.
  * **Tipo de Contrato:** Clientes com contratos mensais (`Month-to-month`) possuem uma taxa de churn significativamente maior (**42.7%**).
  * **Tempo de Permanência (Tenure):** Clientes que cancelam possuem um tempo médio de permanência muito menor (**18.0 meses**) em comparação com os que ficam (**37.6 meses**).

## 💡 Recomendações

Com base nos insights, as seguintes ações são recomendadas para reduzir o churn:

1.  **Programa de Fidelização:** Criar incentivos e benefícios para clientes com contratos de longo prazo (anual, bianual).
2.  **Onboarding Eficiente:** Melhorar o processo de integração de novos clientes para aumentar o engajamento inicial e diminuir o churn precoce.
3.  **Incentivo a Pagamentos Automáticos:** Oferecer pequenos descontos para clientes que optam por débito automático, método associado a menor churn.
4.  **Campanhas de Retenção:** Desenvolver campanhas de marketing direcionadas para clientes de alto risco (ex: baixo tenure, contrato mensal).
5.  **Sistema de Alertas:** Criar um sistema que identifique proativamente clientes com comportamento propenso ao cancelamento.
6.  **Benefícios por Tempo de Casa:** Oferecer vantagens progressivas de acordo com o tempo de permanência do cliente.

## 🛠️ Tecnologias Utilizadas

  * **Python 3**
  * **Pandas**
  * **NumPy**
  * **Matplotlib**
  * **Seaborn**
  * **Requests**
  * **Jupyter Notebook**

## 🚀 Como Executar o Projeto

1.  **Pré-requisitos:**

      * Python 3.x instalado.
      * `pip` (gerenciador de pacotes do Python).

2.  **Clone o repositório (opcional):**

    ```bash
    git clone <URL_DO_REPOSITORIO>
    cd <NOME_DO_REPOSITORIO>
    ```

3.  **Instale as dependências:**

    ```bash
    pip install pandas numpy matplotlib seaborn requests jupyterlab
    ```

4.  **Execute o Jupyter Notebook:**

    ```bash
    jupyter notebook "TelecomX_BR (1).ipynb"
    ```

## 📂 Fonte dos Dados

Os dados foram extraídos do seguinte link, como parte do Challenge de Data Science da Alura:

  * **URL:** `https://raw.githubusercontent.com/ingridcristh/challenge2-data-science/main/TelecomX_Data.json`
