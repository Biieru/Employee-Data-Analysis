# BCB Merchant Analytics

**Pipeline ETL e análise de estabelecimentos credenciados a cartões no Brasil.**

Projeto de engenharia e análise de dados desenvolvido em Python, utilizando dados públicos do Banco Central do Brasil (BCB). A aplicação extrai informações sobre estabelecimentos credenciados e ativos, organiza os dados com pandas e permite sua exportação para CSV e bancos de dados relacionais.

O repositório também inclui um notebook de análise e um relatório desenvolvido em Power BI.

## Objetivo

Explorar dados do mercado brasileiro de pagamentos eletrônicos, aplicando conceitos de extração, transformação, armazenamento e visualização de dados.

Os dados disponibilizados pelo BCB permitem investigar a quantidade de estabelecimentos credenciados e ativos, considerando diferentes bandeiras, funções dos cartões e períodos trimestrais.

## Tecnologias

| Tecnologia | Aplicação |
|---|---|
| Python | Desenvolvimento do pipeline |
| pandas | Processamento e organização dos dados |
| requests | Consumo da API REST |
| SQLite | Armazenamento relacional |
| SQLAlchemy e PyMySQL | Integração opcional com MySQL |
| Jupyter Notebook | Exploração e análise de dados |
| Power BI | Relatórios e visualização |

## Funcionamento

O projeto segue um fluxo ETL (*Extract, Transform, Load*) dividido em três etapas.

**1. Extração**

Consulta à API pública do Banco Central do Brasil, utilizando o serviço `EstabCredTransDA` e um trimestre de referência.

**2. Transformação**

Conversão da resposta JSON em um DataFrame pandas, organizando os registros para armazenamento e análise.

**3. Carregamento**

Persistência dos dados processados em diferentes formatos:

- CSV, para interoperabilidade e análises externas.
- SQLite, para consultas em banco de dados relacional.
- MySQL, como alternativa implementada no módulo de persistência, mas não habilitada na execução principal.

## Estrutura do projeto

```text
EstabelecimentosCredenciados/
├── main.py
├── relatorio_estabelecimentos.ipynb
├── Relatorio Estabelecimentos Credenciados.pbix
├── requirements.txt
├── README.md
└── src/
    ├── extractTransform.py
    ├── load.py
    └── datasets/
```

O módulo `extractTransform.py` concentra a consulta à API e a transformação da resposta em DataFrame.

O módulo `load.py` disponibiliza funções independentes para exportação em CSV, SQLite e MySQL.

## Dados analisados

| Campo | Descrição |
|---|---|
| `trimestre` | Período de referência |
| `bandeira` | Bandeira do cartão |
| `funcaoCartao` | Modalidade do cartão |
| `qtdEstabCredenciados` | Quantidade de estabelecimentos credenciados |
| `qtdEstabAtivos` | Quantidade de estabelecimentos ativos |

**Fonte:** [Banco Central do Brasil, Dados Abertos](https://dadosabertos.bcb.gov.br/dataset/estatisticas-meios-pagamentos/resource/523552bd-477b-4dcf-93aa-48ffc3c7a41b)

## Como executar

### 1. Clonar o repositório

```bash
git clone https://github.com/Biieru/EstabelecimentosCredenciados.git
cd EstabelecimentosCredenciados
```

### 2. Instalar as dependências

```bash
pip install -r requirements.txt
```

### 3. Executar o pipeline

```bash
python main.py
```

Por padrão, a execução utiliza o trimestre `20241`, correspondente ao primeiro trimestre de 2024.

Para consultar outro período, altere o argumento da função `estabelecimentos_credenciados()` em `main.py`.

O programa consulta a API e grava os dados em arquivos CSV e SQLite dentro de `src/datasets/`.

**Observação:** a exportação para MySQL está disponível no código, mas desabilitada por padrão. Sua utilização exige um banco configurado e credenciais válidas.

## Análise e visualização

Além do pipeline, o projeto inclui dois materiais complementares:

**Jupyter Notebook**

Arquivo `relatorio_estabelecimentos.ipynb`, destinado à exploração e análise dos dados.

**Power BI**

Arquivo `Relatorio Estabelecimentos Credenciados.pbix`, contendo o relatório de visualização do projeto.

Esses materiais complementam o processo de coleta e armazenamento, permitindo explorar os dados em diferentes ferramentas.

## Aprendizados

O desenvolvimento deste projeto proporcionou experiência prática em:

- Integração com APIs REST e consumo de dados públicos.
- Tratamento de respostas JSON com pandas.
- Construção de pipelines ETL em Python.
- Persistência e organização de dados em SQLite.
- Integração com bancos relacionais utilizando SQLAlchemy.
- Separação de responsabilidades em módulos Python.
- Exploração e apresentação de dados utilizando Jupyter e Power BI.

## Limitações e melhorias futuras

A implementação atual utiliza um trimestre fixo e executa a extração sob demanda.

Possíveis evoluções incluem:

- Parametrização do trimestre por linha de comando.
- Coleta automatizada de múltiplos períodos.
- Tratamento de erros HTTP e indisponibilidade da API.
- Validação de dados e testes automatizados.
- Padronização das configurações de conexão.
- Documentação visual dos indicadores produzidos no Power BI.

## Autores

Projeto acadêmico desenvolvido por:

- **Gabriel Coelho de Araújo** | [GitHub](https://github.com/Biieru)
- **Cauan Warlley**

## Fonte e licença

Os dados utilizados são disponibilizados publicamente pelo Banco Central do Brasil.

Este repositório contém um arquivo `LICENSE` com os termos de licenciamento do projeto.

---

**Python · ETL · SQL · Análise de Dados · Power BI**
