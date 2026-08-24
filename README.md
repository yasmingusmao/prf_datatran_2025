# Projeto PRF 2025: Pipeline de Preparação de Dados

Este projeto consiste em um pipeline de engenharia de dados focado em processar, limpar e enriquecer os registros abertos de acidentes da Polícia Rodoviária Federal (PRF) de 2025. 

O script transforma o arquivo bruto da PRF em bases de dados sólidas, isolando as informações para não comprometer análises futuras.

---

## Objetivo

Preparar os dados de acidentes rodoviários para três frentes principais:
*   **Análise Exploratória (EDA):** Extração inicial de *insights* e estatísticas.
*   **Business Intelligence (BI):** Consumo dos dados estruturados em *dashboards* (Power BI).
*   **Machine Learning (ML):** Treinamento de algoritmos de Inteligência Artificial (Árvore de Decisão) para prever a letalidade de acidentes.

---

## O que o pipeline faz?

*   **Limpeza e Tratamento:** Remove duplicidades exatas, trata valores nulos com regras de negócio e padroniza formatos e textos.
*   **Criação de Variáveis (*Feature Engineering*):** Cria agrupamentos de datas, turnos de horário e, principalmente, a variável-alvo **`acidente_fatal`** (marcando 1 para acidentes com óbito e 0 para acidentes sem óbito).
*   **Segurança Preditiva:** Aplica regras anti-*data leakage* (vazamento de dados), garantindo que colunas que "entregam" o resultado do acidente (como quantidade de mortos ou feridos) não entrem na base de modelagem da IA.

---

## Tecnologias e Bibliotecas

O projeto foi construído em Python e não exige hardwares especiais, rodando perfeitamente no Google Colab ou localmente.

| Biblioteca | Uso no Projeto |
| :--- | :--- |
| **pandas** | Leitura robusta, limpeza, transformações estruturais e exportação das bases. |
| **numpy** | Processamento rápido de regras condicionais para criação de novos indicadores. |
| **matplotlib** | Geração de gráficos de conferência (ex: distribuição da variável-alvo). |
| **pathlib** | Criação automática da estrutura de pastas e gestão segura de caminhos de arquivos. |
| **datetime** | Extração de informações de calendário (mês, trimestre, fim de semana) e geração de logs. |
| **unicodedata** | Remoção de acentos e caracteres especiais durante a padronização dos dados. |

---

## O que é gerado ao final? (Entregáveis)

Ao rodar o notebook, ele automaticamente estrutura as pastas e devolve os seguintes ativos na pasta `dados_tratados/`:

1.  **`base_analitica_prf_2025.csv`:** Tabela completa, contendo todas as vítimas e indicadores de gravidade. Feita sob medida para criação de painéis visuais e relatórios.
2.  **`base_modelavel_prf_2025.csv`:** Tabela restrita para os algoritmos de Machine Learning. Contém apenas características que existiam *antes* ou *durante* o acidente (clima, via, horário) mais o alvo a ser previsto.
3.  **`dicionario_variaveis_modulo4.csv`:** Arquivo de documentação explicando cada nova coluna criada no projeto.

---

## Como Executar

1. Abra o arquivo do notebook no seu ambiente (Google Colab recomendado).
2. Rode a primeira célula para que o código crie as pastas do projeto automaticamente.
3. Coloque o arquivo original da PRF (`dados_abertos_prf-datatran2025.csv`) dentro da pasta `dados_brutos/`.
4. Execute o restante do notebook de cima para baixo. Tudo será salvo e exportado de forma automática.
