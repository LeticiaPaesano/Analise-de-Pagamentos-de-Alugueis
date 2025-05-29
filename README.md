# 🏢 Administração de Condomínios – Análise de Pagamentos de Aluguéis

## 🎯 Objetivo

Analisar dados históricos de pagamento de aluguéis de unidades residenciais para identificar atrasos e apoiar a gestão financeira do condomínio.

---

## 📁 Fonte de Dados

- Arquivo: `dados_locacao_imoveis.json`
- Estrutura: JSON com lista de registros por apartamento contendo:
  - Datas combinadas para pagamento (`datas_combinadas_pagamento`)
  - Datas reais de pagamento (`datas_de_pagamento`)
  - Valores pagos (`valor_aluguel`)

---

## ⚙️ Processo de ETL

### 🔹 Extração
Leitura do arquivo JSON utilizando a biblioteca `json`.

### 🔹 Transformação
- Normalização dos dados: cada pagamento se torna uma linha única.
- Conversão de:
  - Datas para formato `datetime`;
  - Valores para tipo `float`.
- Cálculo dos dias de atraso entre a data combinada e a data real.
- Criação da coluna `status_pagamento` com os valores:
  - `"Em dia"`
  - `"Em atraso"`

### 🔹 Carga
Exportação de duas bases `.csv`:
- `pagamentos_tratados.csv` – base detalhada com todos os registros;
- `resumo_por_apartamento.csv` – total por apartamento e atrasos consolidados.

---

## 📊 Análises Realizadas

### 1. Total Recebido por Apartamento
Valor total recebido em aluguéis por apartamento. 

### 2. Total de Dias em Atraso por Apartamento
Soma de todos os dias de atraso acumulados por unidade.

### 3. Distribuição Geral dos Dias em Atraso
Gráfico de densidade com `seaborn` para observar a dispersão dos dias de atraso. 

### 4. Quantidade de Atrasos por Apartamento
Gráfico de barras horizontais com a frequência de atrasos por unidade.

---

## 📈 Exemplos de Visualizações

Todos os gráficos foram padronizados com o tamanho `(10, 5)` para garantir consistência visual:

### 🔸 KDE – Estimativa de Densidade dos Dias de Atraso
```python
import seaborn as sns
plt.figure(figsize=(10, 5))
sns.kdeplot(df_locacao['dias_de_atraso'], fill=True, color='purple')
```
![image](https://github.com/user-attachments/assets/1e414914-9fae-41cf-91ef-54d3d2e2cc96)

### 🔸 Total Recebido por Apartamento
```python
plt.figure(figsize=(10, 5))
df_resumo.sort_values('total_pago').plot(kind='bar')
```
![image](https://github.com/user-attachments/assets/44b771ef-a9e9-425e-ad06-04f6b814b9d4)

---

## 📌 Indicadores

- Taxa de inadimplência:
Proporção de pagamentos com atraso em relação ao total de pagamentos registrados.
```python
taxa_inadimplencia = total_atrasos / total_lancamentos
```
```matlab
Taxa de inadimplência: 83.33%
```
---

## 💾 Arquivos Exportados

`pagamentos_tratados.csv` – dados normalizados com atraso e status

`resumo_por_apartamento.csv` – consolidação por unidade residencial

---

## 🛠️ Tecnologias Utilizadas
Python 3.10+

pandas

matplotlib

seaborn

json

