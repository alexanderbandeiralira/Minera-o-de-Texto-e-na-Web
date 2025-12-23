# 🛒 Pipeline ETL & Web Scraping - Dados de E-commerce

![Python](https://img.shields.io/badge/Python-3.10-blue?style=for-the-badge&logo=python)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas)
![BeautifulSoup](https://img.shields.io/badge/BeautifulSoup-Scraping-yellow?style=for-the-badge)

## 📌 Visão Geral

Este projeto consiste em um pipeline **ETL (Extract, Transform, Load)** desenvolvido para processar dados brutos de HTML de um e-commerce fictício. O objetivo é estruturar informações desorganizadas, aplicar regras de negócio para precificação e padronizar os dados para análise posterior.

O projeto simula um cenário real onde dados são extraídos do front-end ou de um crawler e precisam ser limpos antes de serem armazenados.

---

## ⚙️ Arquitetura do Pipeline

O processo foi dividido em três estágios clássicos de engenharia de dados:

### 1. Extract (Extração)
Utilizando a biblioteca **BeautifulSoup**, o script faz o parsing do HTML bruto (`HTML_DATA`).
* **Filtro de Integridade:** Foi implementada uma regra rígida onde produtos sem a tag de preço (`<p class="price">`) são identificados e **descartados** imediatamente, gerando um log de alerta.
* **Coleta:** Extração de ID, Nome, Preço bruto, Avaliação, Imagem, Data e Desconto.

### 2. Transform (Transformação)
Com os dados extraídos, utiliza-se **Pandas** e **Regex** para limpeza e tipagem:
* **Limpeza de Strings:** Remoção de símbolos de moeda (`R$`) e percentuais (`% OFF`).
* **Conversão de Tipos:** Transformação de preços e descontos para `float`.
* **Normalização de Avaliação:** Conversão da escala "x/5.0" para uma escala percentual (0-100).
* **Padronização de Data:** Alteração do formato `dd/mm/yyyy` para `dd-mm-yyyy`.
* **Regra de Negócio:** Criação do campo calculado `preco_liquido`, aplicando o desconto sobre o valor original.

### 3. Load (Carga)
Os dados processados e estruturados são exportados para um arquivo CSV (`ofertas_calculadas.csv`), pronto para ser consumido por ferramentas de BI ou outros sistemas.

---

📊 Resultados

A partir de um HTML não estruturado, o pipeline gerou a seguinte estrutura tabular limpa:

| nome | preco_numerico | desconto_percentual | preco_liquido | avaliacao_percentual | data |
| :--- | :--- | :--- | :--- | :--- | :--- |
| Smartphone X10 | 1999.99 | 10.0 | 1799.99 | 90.0 | 27-11-2025 |
| Notebook Ultraline | 4500.00 | 0.0 | 4500.00 | 96.0 | 28-11-2025 |
| Fone Bluetooth Pro | 549.50 | 5.0 | 522.02 | 78.0 | 28-11-2025 |
| Smartwatch Z | 1250.00 | 20.0 | 1000.00 | 100.0 | 27-11-2025 |


👨‍💻 Autor

Alexander Lira Data Analyst | Python | Engenharia de Dados
