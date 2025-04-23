# Delta Lake com Apache Spark

Este documento descreve a implementação e uso do Delta Lake com Apache Spark, demonstrando operações básicas de manipulação de dados.

## Configuração do Ambiente

### SparkSession
```python
spark = ( 
    SparkSession
    .builder
    .master("local[*]")
    .config("spark.jars.packages", "io.delta:delta-core_2.12:2.4.0")
    .config("spark.sql.extensions", "io.delta.sql.DeltaSparkSessionExtension")
    .config("spark.sql.catalog.spark_catalog", "org.apache.spark.sql.delta.catalog.DeltaCatalog")
    .getOrCreate() 
)
```

## Estrutura dos Dados

### Schema da Tabela
```python
schema = (
    StructType([
        StructField("ID_CLIENTE",     StringType(),True),
        StructField("NOME_CLIENTE",   StringType(),True),
        StructField("UF",             StringType(),True),
        StructField("STATUS",         StringType(),True),
        StructField("LIMITE_CREDITO", FloatType(), True)
    ])
)
```

## Operações Demonstradas

### 1. Criação de Dados Iniciais
- Criação de um DataFrame com dados de clientes
- Campos: ID_CLIENTE, NOME_CLIENTE, UF, STATUS, LIMITE_CREDITO
- Exemplo de dados:
  - ID001, CLIENTE_X, SP, ATIVO, 250000.00
  - ID002, CLIENTE_Y, SC, INATIVO, 400000.00
  - ID003, CLIENTE_Z, DF, ATIVO, 1000000.00

### 2. Salvamento em Formato Delta
```python
df.write
  .format("delta")
  .mode('overwrite')
  .save("./dataset_delta/CLIENTES")
```

### 3. Merge de Dados
- Demonstração de operação MERGE (UPSERT)
- Atualização de registros existentes
- Inserção de novos registros
- Exemplo de dados atualizados:
  - ID001: Status alterado para INATIVO e limite zerado
  - ID002: Status alterado para ATIVO
  - ID004: Novo cliente inserido

### 4. Deleção de Dados
```python
deltaTable.delete("LIMITE_CREDITO < 400000.0")
```
- Remove registros com limite de crédito menor que 400.000

## Benefícios do Delta Lake

1. **ACID Transactions**
   - Garantia de atomicidade nas operações
   - Consistência dos dados

2. **Time Travel**
   - Capacidade de visualizar versões anteriores dos dados
   - Rollback de operações

3. **Schema Evolution**
   - Suporte a evolução do schema
   - Compatibilidade com mudanças na estrutura

4. **Auditoria**
   - Rastreamento de todas as operações
   - Histórico de modificações

## Boas Práticas

1. **Versionamento**
   - Manter controle das versões dos dados
   - Documentar mudanças significativas

2. **Otimização**
   - Compactação periódica dos dados
   - Limpeza de arquivos antigos

3. **Monitoramento**
   - Acompanhar o tamanho das tabelas
   - Verificar performance das operações 