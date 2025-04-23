# Data Lake com Apache Spark, Delta Lake e Apache Iceberg

Este projeto demonstra a implementação de um Data Lake usando Apache Spark com os formatos de tabela Delta Lake e Apache Iceberg, incluindo exemplos de operações de manipulação de dados e comparações entre os dois formatos.

## Pré-requisitos

- Python 3.12 ou superior
- Poetry (gerenciador de pacotes Python)
- Java 11 ou superior (necessário para Apache Spark)
- Hadoop 3.0.0 (Necessário para o Apache Iceberg)
- JDK 8 (necessário para Hadoop)
- Git

## Instalação

### 1. Configuração do Ambiente Python

Primeiro, certifique-se de ter o Python 3.12+ instalado:
```bash
python --version
```

Se necessário, instale o Python 3.12:
- **macOS**: `brew install python@3.12`
- **Linux**: Use o gerenciador de pacotes da sua distribuição
- **Windows**: Baixe o instalador do [python.org](https://www.python.org/downloads/)

### 2. Instalação do Poetry

#### macOS/Linux:
```bash
curl -sSL https://install.python-poetry.org | python3 -
```

#### Windows (PowerShell):
```powershell
(Invoke-WebRequest -Uri https://install.python-poetry.org -UseBasicParsing).Content | py -
```

Verifique a instalação:
```bash
poetry --version
```

### 3. Configuração do Java e Hadoop

Certifique-se de ter o Java 11+ instalado:
```bash
java -version
```

Configure a variável JAVA_HOME:
- **macOS/Linux**: Adicione ao ~/.bashrc ou ~/.zshrc:
  ```bash
  export JAVA_HOME=$(/usr/libexec/java_home -v 11)
  export PATH=$JAVA_HOME/bin:$PATH
  export HADOOP_HOME=$(/usr/libexec/hadoop)
  ```
- **Windows**: Configure através das Variáveis de Ambiente do Sistema

### 4. Clone do Repositório

```bash
git clone https://github.com/your-username/datalake-with-spark-and-iceberg.git
cd datalake-with-spark-and-iceberg
```

### 5. Configuração do Projeto

1. Instale as dependências do projeto:
```bash
poetry install
```

2. Ative o ambiente virtual:
```bash
poetry shell
```

3. Configure o kernel do Jupyter:
```bash
poetry run python -m ipykernel install --user --name=datalake-with-spark-and-iceberg
```

## Estrutura do Projeto

```
datalake-with-spark-and-iceberg/
├── documentation/           # Documentação detalhada
│   ├── delta/             # Documentação Delta Lake
│   └── iceberg/           # Documentação Apache Iceberg
├── notebooks/             # Notebooks Jupyter
│   ├── dataset_delta/    # Dados e exemplos Delta Lake
│   ├── dataset_iceberg/  # Dados e exemplos Apache Iceberg
│   ├── spark_delta.ipynb # Operações Delta Lake
│   └── spark-iceberg.ipynb # Operações Apache Iceberg
├── src/                  # Código fonte
│   └── config/          # Arquivos de configuração
├── pyproject.toml       # Configuração do Poetry
└── README.md           # Este arquivo
```

## Como Usar

### 1. Iniciando o Ambiente

1. Ative o ambiente virtual:
```bash
poetry shell
```

2. Inicie o JupyterLab:
```bash
poetry run jupyter lab
```

### 2. Executando os Notebooks

1. No JupyterLab:
   - Navegue até a pasta `notebooks/`
   - Abra `spark_delta.ipynb` ou `spark-iceberg.ipynb`
   - Selecione o kernel `datalake-with-spark-and-iceberg`
   - Execute as células em sequência

### 3. Documentação

A documentação detalhada está disponível em:
- Delta Lake: `documentation/delta/index.md`
- Apache Iceberg: `documentation/iceberg/index.md`

Para visualizar a documentação localmente:
```bash
poetry run mkdocs serve
```
Acesse `http://127.0.0.1:8000` no navegador.

## Dependências Principais

```toml
[tool.poetry.dependencies]
python = "^3.12"
pyspark = ">=3.5.5,<4.0.0"
delta-spark = ">=3.0.0,<4.0.0"
jupyterlab = ">=4.4.0,<5.0.0"
ipykernel = ">=6.29.5,<7.0.0"
mkdocs = ">=1.5.0,<2.0.0"
mkdocs-material = ">=9.0.0,<10.0.0"
mkdocstrings = ">=0.24.0,<1.0.0"
```

## Solução de Problemas

### Erro: "No module named 'pyspark'"
1. Verifique se está usando o kernel correto:
   ```bash
   poetry run jupyter kernelspec list
   ```
2. Reinstale as dependências:
   ```bash
   poetry install
   ```
3. Reconfigure o kernel:
   ```bash
   poetry run python -m ipykernel install --user --name=datalake-with-spark-and-iceberg
   ```

### Erro de Java
1. Verifique a instalação do Java:
   ```bash
   java -version
   ```
2. Configure JAVA_HOME:
   ```bash
   echo $JAVA_HOME
   ```
3. Se necessário, reinstale o Java 11+

### Erro de Memória do Spark
1. Ajuste as configurações de memória no notebook:
   ```python
   spark.conf.set("spark.driver.memory", "2g")
   spark.conf.set("spark.executor.memory", "2g")
   ```

## Contribuindo

1. Fork o repositório
2. Crie sua branch de feature (`git checkout -b feature/nova-feature`)
3. Commit suas mudanças (`git commit -m 'Adiciona nova feature'`)
4. Push para a branch (`git push origin feature/nova-feature`)
5. Abra um Pull Request

## Referências Bibliográficas

- https://datawaybr.medium.com/como-sair-do-zero-no-delta-lake-em-apenas-uma-aula-d152688a4cc8
- https://medium.com/@r.yamnych/apache-iceberg-to-pyspark-by-example-c9d52843694a

## Licença

Este projeto está licenciado sob a Licença MIT - veja o arquivo LICENSE para detalhes. 
