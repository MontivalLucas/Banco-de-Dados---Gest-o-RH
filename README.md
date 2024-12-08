# Projeto de Implementação de Banco de Dados - Gestão de Recursos Humanos

## Objetivo

O objetivo deste projeto foi implementar um banco de dados para a gestão de recursos humanos, utilizando o SGBD Oracle. O banco foi projetado com base em um Modelo Físico de Dados (MFD) fornecido, e inclui a criação de tabelas, definição de chaves primárias e estrangeiras, aplicação de restrições e inserção de dados coerentes. O trabalho contempla os seguintes passos:

1. **Criação de Estruturas de Banco de Dados** (DDL - Data Definition Language)
2. **Inserção de Dados** (DML - Data Manipulation Language)
3. **Validação e Testes** no Oracle

Este README fornece uma explicação detalhada sobre as tabelas, suas colunas, restrições, relacionamentos e a estrutura do repositório.

---

## Estrutura do Banco de Dados

### 1. **TABELAS E SUAS COLUNAS**

#### **DEPARTAMENTOS**
A tabela **DEPARTAMENTOS** armazena os dados dos departamentos da empresa.

| Coluna            | Tipo de Dados     | Restrição                               | Descrição                          |
|-------------------|-------------------|-----------------------------------------|------------------------------------|
| **DEPARTAMENTO_ID** | `NUMBER(38, 0)`    | `NOT NULL`, `PRIMARY KEY`               | Identificador único do departamento. |
| **NOME**            | `VARCHAR2(100)`    | `NOT NULL`                              | Nome do departamento.              |
| **LOCALIZACAO**     | `VARCHAR2(100)`    | `NOT NULL`                              | Localização do departamento.       |

#### **FUNCIONARIOS**
A tabela **FUNCIONARIOS** contém informações sobre os funcionários da empresa.

| Coluna             | Tipo de Dados      | Restrição                               | Descrição                                |
|--------------------|--------------------|-----------------------------------------|------------------------------------------|
| **FUNCIONARIO_ID**  | `NUMBER(38, 0)`     | `NOT NULL`, `PRIMARY KEY`               | Identificador único do funcionário.      |
| **NOME**            | `VARCHAR2(100)`     | `NOT NULL`                              | Nome do funcionário.                     |
| **DATA_NASCIMENTO** | `DATE`              | `NOT NULL`                              | Data de nascimento do funcionário.       |
| **CARGO**           | `VARCHAR2(100)`     | `NOT NULL`                              | Cargo do funcionário.                    |
| **SALARIO**         | `NUMBER(10, 2)`     | `NOT NULL`                              | Salário do funcionário.                  |
| **DATA_ADMISSAO**   | `DATE`              | `NOT NULL`                              | Data de admissão do funcionário.         |
| **DEPARTAMENTO_ID** | `NUMBER(38, 0)`     | `NOT NULL`, `FOREIGN KEY`               | Identificador do departamento do funcionário. Refere-se à tabela **DEPARTAMENTOS**. |

#### **AVALIACOES_DESEMPENHO**
A tabela **AVALIACOES_DESEMPENHO** contém informações sobre as avaliações de desempenho dos funcionários.

| Coluna            | Tipo de Dados     | Restrição                               | Descrição                          |
|-------------------|-------------------|-----------------------------------------|------------------------------------|
| **AVALIACAO_ID**  | `NUMBER(38, 0)`    | `NOT NULL`, `PRIMARY KEY`               | Identificador único da avaliação.  |
| **FUNCIONARIO_ID**| `NUMBER(38, 0)`    | `NOT NULL`, `FOREIGN KEY`               | Identificador do funcionário avaliado. Refere-se à tabela **FUNCIONARIOS**. |
| **DATA_AVALIACAO**| `DATE`             | `NOT NULL`                              | Data da avaliação.                 |
| **NOTA**          | `NUMBER(4, 2)`     | `CHECK (NOTA BETWEEN 0 AND 10)`        | Nota da avaliação (0 a 10).         |
| **COMENTARIOS**   | `VARCHAR2(4000)`   |                                         | Comentários sobre a avaliação.      |

#### **FOLHA_PAGAMENTO**
A tabela **FOLHA_PAGAMENTO** registra os pagamentos dos funcionários, incluindo salário, descontos e salário líquido.

| Coluna            | Tipo de Dados     | Restrição                               | Descrição                          |
|-------------------|-------------------|-----------------------------------------|------------------------------------|
| **PAGAMENTO_ID**  | `NUMBER(38, 0)`    | `NOT NULL`, `PRIMARY KEY`               | Identificador único do pagamento.  |
| **FUNCIONARIO_ID**| `NUMBER(38, 0)`    | `NOT NULL`, `FOREIGN KEY`               | Identificador do funcionário. Refere-se à tabela **FUNCIONARIOS**. |
| **DATA_PAGAMENTO**| `DATE`             | `NOT NULL`                              | Data do pagamento.                 |
| **SALARIO_BRUTO** | `NUMBER(10, 2)`    | `NOT NULL`                              | Valor do salário bruto.             |
| **DESCONTOS**     | `NUMBER(10, 2)`    | `NOT NULL`                              | Valor total de descontos.          |
| **SALARIO_LIQUIDO**| `NUMBER(10, 2)`   | `NOT NULL`                              | Valor do salário líquido.           |

---

### 2. **RELACIONAMENTOS ENTRE AS TABELAS**

- **FUNCIONARIOS → DEPARTAMENTOS**: Cada funcionário pertence a um único departamento. A tabela **FUNCIONARIOS** tem uma chave estrangeira (**DEPARTAMENTO_ID**) que se refere à tabela **DEPARTAMENTOS**.
- **AVALIACOES_DESEMPENHO → FUNCIONARIOS**: Cada avaliação de desempenho está vinculada a um funcionário. A tabela **AVALIACOES_DESEMPENHO** possui a chave estrangeira (**FUNCIONARIO_ID**) que faz referência à tabela **FUNCIONARIOS**.
- **FOLHA_PAGAMENTO → FUNCIONARIOS**: Cada pagamento está relacionado a um funcionário. A tabela **FOLHA_PAGAMENTO** tem a chave estrangeira (**FUNCIONARIO_ID**) que referencia a tabela **FUNCIONARIOS**.

---

## Scripts DDL (Data Definition Language)

### **estrutura.sql**
Este script contém os comandos para criar as tabelas, definir chaves primárias e estrangeiras, e aplicar as restrições necessárias para garantir a integridade referencial e a validade dos dados.

1. **Criação de Tabelas**: Definição das colunas e tipos de dados.
2. **Definição de Chaves**: Criação de chaves primárias e estrangeiras.
3. **Restrições**: Aplicação de restrições como `NOT NULL`, `CHECK`, `DEFAULT`, e `UNIQUE`.

---

## Scripts DML (Data Manipulation Language)

### **dados.sql**
Este script contém os comandos para inserir dados nas tabelas, respeitando as restrições e os relacionamentos definidos no Modelo Físico de Dados.

1. **Inserção de Dados**: Cada tabela foi populada com dados representativos.
2. **Relacionamentos**: As inserções garantem que os dados de uma tabela estejam corretamente relacionados às tabelas associadas.

---

## Como Executar os Scripts no Oracle

1. **Conectar-se ao Oracle**: Use o SQL*Plus ou SQL Developer para conectar-se ao seu banco de dados Oracle.
2. **Executar o Script DDL**:
   - No SQL*Plus: `@estrutura.sql`
   - No SQL Developer: Execute diretamente no painel de SQL.
3. **Executar o Script DML**:
   - Após a criação das tabelas, execute o script `dados.sql` para inserir os dados.

---

## Validação no Oracle

Durante os testes, foi validado o sucesso da execução dos scripts, tanto para a criação das tabelas quanto para a inserção dos dados:

1. **Testes de Criação das Tabelas**: As tabelas foram criadas corretamente, com todas as restrições aplicadas.
2. **Testes de Inserção de Dados**: Dados coerentes foram inseridos nas tabelas, com referências entre elas respeitadas.
3. **Consultas de Validação**:
   ```sql
   SELECT * FROM USR_GESTAO_RH.DEPARTAMENTOS;
   SELECT * FROM USR_GESTAO_RH.FUNCIONARIOS;
   SELECT * FROM USR_GESTAO_RH.AVALIACOES_DESEMPENHO;
   SELECT * FROM USR_GESTAO_RH.FOLHA_PAGAMENTO;



---

## Divisão Participantes do Grupo


Montival Lucas ------- itens 1, 2, 4, 5, 6.

Yuji Ihara ------------- itens 2, 3, 4, 6.


1. **Objetivo e Estrutura**:Modelagem inicial escrita com base no objetivo do projeto, as tabelas e seus relacionamentos.
2. **Scripts DDL e DML**: Criação das tabelas, as chaves e as inserções de dados.
3. **Como Executar**: Instruções sobre como rodar os scripts no Oracle.
4. **Validação**: Informa os testes feitos no Oracle para garantir a correção.
5. **Estrutura do Repositório**: Estruturação do repositório e como está organizado.
6. **Conclusão**: Revisão Geral sobre a entrega do trabalho.
