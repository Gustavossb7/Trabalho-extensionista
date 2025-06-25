# Trabalho Extensionista — Coleta, Análise e Preparação de Dados

**Grupo**: Gustavo Bortolon, Lucas Ulson, Victor Cruz e Willian Klein.

Este repositório contém os códigos e artefatos desenvolvidos no trabalho extensionista da disciplina de *Coleta, Análise e Preparação de Dados*.

## Conjuntos de Dados Utilizados

Foram selecionados dois conjuntos de dados principais para análise e integração:

- **Microdados do Censo da Educação Superior**  
- **Microdados do ENADE 2021**

Dentro desses conjuntos, os seguintes arquivos foram utilizados:

- Do **Censo**:
  - `MICRODADOS_CADASTRO_CURSOS_2021.CSV`
  - `MICRODADOS_CADASTRO_IES_2021.CSV`

- Do **ENADE**:
  - `microdados2021_arq1.txt`
  - `microdados2021_arq3.txt`
  - `microdados2021_arq14.txt`

## Estrutura do Código

O repositório inclui scripts Python desenvolvidos para realizar o tratamento, integração e análise exploratória dos dados, de forma a gerar um dataset final consistente e preparado para visualização e análise no Power BI.

### `analise_exploratoria.py`

Este script realiza uma análise exploratória **focada no perfil dos alunos do Grupo 906 (Licenciatura em Letras - Português e Espanhol)**, com o objetivo de entender a distribuição das modalidades, a situação dos registros de notas e a distribuição de renda familiar.

Entre as análises realizadas:

- Total de registros na base filtrada  
- Distribuição de alunos entre presencial e EAD  
- Proporção de valores ausentes nas principais variáveis (`NT_GER`, `QE_I08`)  
- Frequência das faixas de renda familiar (variável `QE_I08`)  
- Média das notas gerais (`NT_GER`) por modalidade  
- Quantidade de valores ausentes/presentes por modalidade  
- Gráfico de barras para distribuição das faixas de renda  
- Boxplot das notas por modalidade

★ Esta análise foi essencial para entender melhor o perfil da base de dados após a filtragem e preparar os dados para a etapa de integração e geração do dataset final para o dashboard.

### `equilibrio.py`

O script `equilibrio.py` é responsável por identificar os grupos de curso que apresentam o **maior equilíbrio na quantidade de alunos entre as modalidades presencial e EAD**.  

Ele combina dados do ENADE referentes às modalidades e notas, agrupa por `CO_GRUPO` e `CO_MODALIDADE`, e calcula a **diferença absoluta entre o número de alunos de cada modalidade**.  

Em seguida, classifica os grupos mais equilibrados, ou seja, aqueles com uma distribuição mais uniforme entre alunos de EAD e presencial.

★ **Com base nesse critério, foi definido o uso do Grupo 906 (Licenciatura em Letras - Português e Espanhol), que apresentou um equilíbrio muito bom entre as modalidades, tornando-se adequado para a análise do trabalho.**

### `dataSetFinal.py`

Este script é responsável por **gerar o dataset final** que será utilizado para visualização no Power BI.  

Ele carrega os dados do ENADE 2021, do Censo da Educação Superior e do Cadastro de IES, realiza a integração entre os conjuntos de dados e aplica os seguintes tratamentos:

- Filtragem para o **Grupo 906** (Licenciatura em Letras - Português e Espanhol), incluindo apenas alunos com nota (`NT_GER`)  
- Integração com informações do Censo, unindo por curso, instituição e modalidade  
- Inclusão da informação de região (`NO_REGIAO_IES`) a partir do Cadastro de IES  
- Seleção das colunas finais relevantes: modalidade, nota geral, faixa de renda e região  
- Geração de um arquivo CSV (`censo_enade_letras2021.csv`), que serve como base para a construção do dashboard no Power BI

★ **Este é o script que consolida e gera o dataset definitivo a ser utilizado na análise e apresentação final do trabalho.**

## Produto Final

Como resultado, foi gerado um dataset final preparado para análise e um dashboard no Power BI (`dashboard.pbix`), que permite a visualização interativa dos dados e a extração de insights relevantes.

O dataset final é o arquivo CSV `censo_enade_letras2021.csv`, contendo as seguintes colunas:

- `CO_MODALIDADE`: Indica a modalidade de ensino do aluno. Valor `1` corresponde a "Presencial", e valor `0` corresponde a "EAD".
- `NT_GER`: Nota geral obtida pelo aluno no ENADE.
- `QE_I08`: Faixa de renda familiar do aluno, conforme a codificação do questionário socioeconômico.
- `NO_REGIAO_IES`: Região geográfica da instituição de ensino superior (IES) do aluno.
