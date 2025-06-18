# 📊 Projeto ETL – Relatório Mundial de Felicidade 2024

## 🚀 Descrição

Projeto de ETL desenvolvido em Python com objetivo de extrair, transformar e carregar dados do **Relatório Mundial de Felicidade de 2024**. O exercício simula uma pipeline simples de dados, aplicando tratamentos e gerando um relatório específico para a América Latina.

---

## 🎯 Objetivo do Projeto

* Ler o relatório global de felicidade.
* Realizar transformações nos dados para padronização e enriquecimento.
* Gerar um relatório segmentado, com foco nos países da América Latina.

---

## 🛠️ Tecnologias e Ferramentas

* Python 3.11
* Pandas
* JupyterLab (ambiente de desenvolvimento)

---

## 📦 Pipeline ETL

### 🔍 Extração (Extract)

* Fonte: Arquivo CSV `World_Happiness_Report_2024.csv`.
* Leitura via `pandas.read_csv()`.

```python
import pandas as pd
df = pd.read_csv('World_Happiness_Report_2024.csv')
```

---

### 🔧 Transformação (Transform)

1. ✅ **Renomeação das colunas** para facilitar a leitura dos dados.
   Exemplo:

   * `'Country name'` → `'pais'`
   * `'Ladder score'` → `'felicidade'`
   * *(Demais colunas foram renomeadas conforme necessidade)*

2. ✅ **Criação da coluna `nivel_felicidade`** com as seguintes regras de negócio:

   * Felicidade > 6.5 → `'Alta'`
   * Felicidade entre 5.0 e 6.5 → `'Média'`
   * Felicidade < 5.0 → `'Baixa'`

```python
def classificar_felicidade(score):
    if score > 6.5:
        return 'Alta'
    elif score >= 5.0:
        return 'Média'
    else:
        return 'Baixa'

df['nivel_felicidade'] = df['felicidade'].apply(classificar_felicidade)
```

3. ✅ **Filtragem dos países da América Latina**.

4. ✅ **Ordenação** do DataFrame do país mais feliz para o menos feliz (`ORDER BY felicidade DESC`).

---

### 💾 Carga (Load)

* O DataFrame tratado da América Latina foi exportado para um arquivo CSV chamado:

```
relatorio_felicidade_latam_2024.csv
```

```python
df_latam.to_csv('relatorio_felicidade_latam_2024.csv', index=False)
```

---

## 📑 Estrutura de Diretórios

```
📁 etl_felicidade_2024/
├──📁 data/                                        # Dados brutos e processados
│   ├── World_Happiness_Report_2024.csv          # Dataset original (fonte)
│   └── relatorio_felicidade_latam_2024.csv      # Dataset processado (LATAM)
├── etl_felicidade.ipynb                         # Notebook com o pipeline ETL
└── README.md                                    # Documentação do projeto

```

---

## 🔗 Dependências

* pandas

Instalação:

```bash
pip install pandas
```

---

## 📈 Resultados

* Arquivo CSV contendo os países da América Latina, classificados por nível de felicidade, com uma coluna adicional (`nivel_felicidade`) que facilita a análise qualitativa.

---

## 🤝 Contribuição

Sinta-se livre para abrir issues, sugerir melhorias ou colaborar com otimizações e novas funcionalidades.

---

## 🏷️ Licença

Este projeto está licenciado sob a licença MIT. Consulte o arquivo `LICENSE` para mais informações.

---