# Apache Iceberg com Spark

Este documento descreve a implementação e uso do Apache Iceberg com Apache Spark, demonstrando operações básicas de manipulação de dados.

## Configuração do Ambiente

### SparkSession
```python
spark = SparkSession.builder \
  .appName("IcebergLocalDevelopment") \
  .config('spark.jars.packages', 'org.apache.iceberg:iceberg-spark-runtime-3.5_2.12:1.6.1') \
  .config("spark.sql.extensions", "org.apache.iceberg.spark.extensions.IcebergSparkSessionExtensions") \
  .config("spark.sql.catalog.local", "org.apache.iceberg.spark.SparkCatalog") \
  .config("spark.sql.catalog.local.type", "hadoop") \
  .config("spark.sql.catalog.local.warehouse", "dataset_iceberg") \
  .getOrCreate()
```

## Estrutura dos Dados

### Schema da Tabela
```sql
CREATE TABLE local.livros_iceberg (
    id INT,
    titulo STRING,
    autor STRING,
    ano_publicacao INT
) USING iceberg
```

## Operações Demonstradas

### 1. Criação de Dados Iniciais
```sql
INSERT INTO local.livros_iceberg VALUES
    (1, '1984', 'George Orwell', 1949),
    (2, 'Dom Casmurro', 'Machado de Assis', 1899),
    (3, 'O Hobbit', 'J.R.R. Tolkien', 1937)
```

### 2. Consulta de Dados
```sql
SELECT * FROM local.livros_iceberg
```

### 3. Atualização de Dados
```sql
UPDATE local.livros_iceberg
SET autor = 'M. de Assis'
WHERE id = 2
```

### 4. Deleção de Dados
```sql
DELETE FROM local.livros_iceberg
WHERE id = 3
```

## Benefícios do Apache Iceberg

1. **Schema Evolution**
   - Adição/remoção de colunas
   - Renomeação de colunas
   - Alteração de tipos de dados

2. **Partition Evolution**
   - Mudança dinâmica de partições
   - Otimização de consultas

3. **Time Travel**
   - Visualização de snapshots anteriores
   - Rollback de operações
   - Auditoria de mudanças

4. **ACID Transactions**
   - Atomicidade
   - Consistência
   - Isolamento
   - Durabilidade

## Recursos Avançados

1. **Snapshots**
   - Versionamento de dados
   - Histórico de modificações
   - Pontos de restauração

2. **Manifests**
   - Lista de arquivos de dados
   - Metadados de partições
   - Estatísticas de dados

3. **Schema Evolution**
   - Compatibilidade retroativa
   - Evolução segura do schema
   - Validação de tipos

## Boas Práticas

1. **Otimização de Consultas**
   - Uso eficiente de partições
   - Compactação de dados
   - Índices apropriados

2. **Manutenção**
   - Limpeza de snapshots antigos
   - Compactação de arquivos
   - Monitoramento de performance

3. **Segurança**
   - Controle de acesso
   - Auditoria de operações
   - Backup de metadados 