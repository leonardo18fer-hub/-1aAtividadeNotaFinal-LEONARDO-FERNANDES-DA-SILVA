# BIG_DATA_PYTHON

# Evolução da Criminalidade em São Gonçalo (RJ): 2014 a 2024

Trabalho Extensionista de **Tópicos de Big Data em Python** (Estácio).

Análise em Python e PySpark dos registros mensais de criminalidade de São Gonçalo (RJ), com tratamento de dados, estatística descritiva, regressão linear e identificação de outliers. O foco é a queda da violência física e o avanço do estelionato.

[![Abrir no Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1cWPmEqlJMHucIkYBSckywNQNqbkSTEjg?usp=sharing)

## Objetivos

1. **Tratar e descrever** a base mensal do ISP-RJ e comparar os indicadores de 2014 com os de 2024 (variação absoluta e percentual).
2. **Ajustar** uma regressão linear simples ao total anual de ocorrências, medindo a tendência e o poder explicativo (R²).
3. **Identificar** o outlier histórico por meio do z-score da variação anual.

## Base de dados

- **Fonte:** [ISP Dados Abertos](https://ispdados.rj.gov.br) (Instituto de Segurança Pública do Rio de Janeiro).
- **Arquivo:** `BaseMunicipioMensal.xlsx` (ocorrências por município e por mês).
- **Tamanho:** 3,03 MB e 61 colunas na base original. Para São Gonçalo, de 2014 a 2024, são 132 registros mensais (11 anos) e 56 indicadores criminais.
- **Conteúdo:** homicídios, roubos, furtos, estelionato, drogas, ameaças e outros.

## Tratamento dos dados

- Padronização dos nomes de colunas com `unicodedata` (NFKD).
- Filtro por município (São Gonçalo) e por período (2014 a 2024).
- Nulos preenchidos com 0 (`fillna`).
- Verificação de duplicidades (nenhuma encontrada).
- Agregação anual com PySpark e conversão para Pandas para a análise.

## Principais resultados

| Análise | Resultado |
|---|---|
| Total anual de ocorrências | média de 101.312,27, mediana de 113.091,00 e desvio padrão de 31.515,17 |
| Homicídio doloso (2014 → 2024) | 345 → 82 (−76,2%) |
| Roubo de rua | 9.783 → 2.018 (−79,3%) |
| Roubo de veículo | 3.892 → 1.558 (−59,9%) |
| Total de roubos | 15.592 → 4.229 (−72,9%) |
| Estelionato | 1.351 → 4.174 (+208,9%) |
| Registros gerais | 47.404 → 29.760 (−37,2%) |
| Regressão linear | Y = −7.889,64·X + 16.030.488 (X = ano, Y = total anual), com R² de 0,6894 |
| Outlier | 2020: 53.563 ocorrências a menos que em 2019, com z-score de −2,36 (\|z\| > 2) |

## Interpretação

- A **violência física caiu** de forma consistente: homicídios dolosos −76,2% e total de roubos −72,9%.
- O **estelionato mais que triplicou** (+208,9%), o que é um indício de que o crime pode estar migrando da rua para o ambiente digital. A base não separa fraude digital, então é uma hipótese.
- A regressão indica queda de cerca de 7.900 ocorrências por ano, e o tempo explica cerca de 69% da variação do total (R² de 0,6894).
- **2020** foi um choque pontual. A hipótese, à luz da teoria das atividades rotineiras, é que as restrições da pandemia reduziram a circulação de pessoas e os registros. Esse ano puxa a média para baixo, por isso a mediana é o centro mais confiável.

## Limitações

- Os dados são agregados por mês e não distinguem estelionato digital de presencial.
- A regressão simples usa apenas 11 pontos anuais.
- O z-score foi calculado sobre a variação anual, com o critério moderado \|z\| > 2.
- A ligação entre a pandemia e o outlier de 2020 é uma hipótese, não uma relação causal comprovada.
- Os totais não são ponderados pela população do município.

## Como executar

1. Clique no botão **Abrir no Colab** acima.
2. Envie o arquivo `BaseMunicipioMensal.xlsx` para o ambiente do Colab (baixado do [ISP Dados Abertos](https://ispdados.rj.gov.br)).
3. Execute as células em ordem (**Ambiente de execução > Executar tudo**).

Para executar localmente, baixe o notebook no Colab (**Arquivo > Fazer download > .ipynb**) e rode:

```bash
pip install pyspark pandas numpy matplotlib seaborn scikit-learn openpyxl
jupyter notebook
```

## Ferramentas

Python, Google Colab, PySpark, Pandas, Scikit-learn, Matplotlib, Seaborn, `unicodedata` e GitHub.

## Próximos passos

- Calcular **taxas por habitante**, usando a população do município em cada ano.
- Separar o **estelionato digital** do presencial para testar a hipótese de migração do crime.
- Testar **modelos de séries temporais** (como ARIMA) e comparar com outros municípios, como Niterói e Maricá.

## Links, slides e roteiros

Relatorio:file:///C:/Users/aluno/Desktop/Relatorio_Extensionista_Criminalidade_SG.pdf



## Autores

**Leonardo Fernandes** e **João Gabriel Teixeira**  
Orientação: Prof.ª Simone Gama
