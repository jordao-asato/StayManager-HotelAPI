# StayManager

Sistema de gerenciamento hoteleiro desenvolvido em Python com integração a banco de dados relacional.

A aplicação permite administrar hotéis, quartos, clientes, reservas e pagamentos, centralizando operações essenciais do setor de hospedagem por meio de uma arquitetura organizada e consultas SQL otimizadas.

---

## Visão Geral

O StayManager foi desenvolvido para auxiliar o gerenciamento de operações de hospedagem, oferecendo funcionalidades para:

- Cadastro de hotéis
- Gerenciamento de quartos
- Cadastro de clientes
- Controle de reservas
- Processamento de pagamentos
- Consultas gerenciais
- Relatórios de ocupação e faturamento

---

## Funcionalidades

### Gestão de Clientes

- Cadastro de clientes
- Consulta de clientes
- Remoção de clientes
- Controle de informações de contato

### Gestão de Hotéis

- Cadastro de hotéis
- Consulta de hotéis
- Controle de categoria
- Informações de localização

### Gestão de Quartos

- Cadastro de quartos
- Controle de disponibilidade
- Classificação por tipo
- Gerenciamento de preços por diária

### Gestão de Reservas

- Criação de reservas
- Controle de check-in
- Controle de check-out
- Status da reserva

### Gestão de Pagamentos

- Registro de pagamentos
- Controle de status financeiro
- Múltiplas formas de pagamento

---

## Arquitetura do Projeto

```text
Application Layer
        │
        ▼
Business Operations
        │
        ▼
Database Connection Layer
        │
        ▼
PostgreSQL Database
```

---

## Estrutura do Projeto

```text
project/

├── db_connection.py
├── db_operations.py
├── Projeto BD.sql
├── hotel.db
├── test_db.py
├── test_crud.py
└── documentation/
```

---

## Modelo de Dados

### Hotel

| Campo     | Tipo    |
| --------- | ------- |
| id_hotel  | Integer |
| nome      | VARCHAR |
| endereco  | VARCHAR |
| telefone  | VARCHAR |
| categoria | VARCHAR |

---

### Quarto

| Campo        | Tipo    |
| ------------ | ------- |
| id_quarto    | Integer |
| id_hotel     | Integer |
| numero       | Integer |
| tipo         | VARCHAR |
| preco_diaria | DECIMAL |
| status       | VARCHAR |

Status possíveis:

- Disponível
- Ocupado
- Manutenção

---

### Cliente

| Campo      | Tipo    |
| ---------- | ------- |
| id_cliente | Integer |
| nome       | VARCHAR |
| cpf        | VARCHAR |
| telefone   | VARCHAR |
| email      | VARCHAR |

---

### Reserva

| Campo         | Tipo    |
| ------------- | ------- |
| id_reserva    | Integer |
| id_cliente    | Integer |
| id_quarto     | Integer |
| data_checkin  | DATE    |
| data_checkout | DATE    |
| status        | VARCHAR |

Status possíveis:

- Ativa
- Cancelada
- Finalizada

---

### Pagamento

| Campo            | Tipo    |
| ---------------- | ------- |
| id_pagamento     | Integer |
| id_reserva       | Integer |
| valor_total      | DECIMAL |
| metodo_pagamento | VARCHAR |
| status_pagamento | VARCHAR |

Métodos disponíveis:

- Cartão
- PIX
- Dinheiro

---

## Tecnologias Utilizadas

- Python
- PostgreSQL
- SQL
- Psycopg2
- Git
- GitHub

---

## Principais Operações

### Inserir Cliente

```python
inserir_cliente(
    "Carlos Silva",
    "123.456.789-00",
    "99998888",
    "carlos@email.com"
)
```

---

### Listar Clientes

```python
listar_clientes()
```

---

### Inserir Hotel

```python
inserir_hotel(
    "Hotel Central",
    "Rua A, 123",
    "1122334455",
    "4 Estrelas",
    "São Paulo",
    "SP"
)
```

---

### Inserir Quarto

```python
inserir_quarto(
    1,
    101,
    "Standard",
    150.00,
    "Disponível"
)
```

---

## Consultas Gerenciais

O sistema possui consultas analíticas para apoio à tomada de decisão.

### Reservas por Hotel

```sql
SELECT
    h.nome,
    COUNT(r.id_reserva)
FROM hotel h
...
```

---

### Taxa de Ocupação

Permite analisar o percentual de ocupação dos quartos por hotel.

### Faturamento por Hotel

```sql
SELECT
    h.nome,
    SUM(p.valor_total)
FROM pagamento p
...
```

---

### Ranking de Clientes

Identifica clientes com maior número de reservas.

---

## Relacionamento Entre Entidades

```text
Hotel
 │
 └── Quarto
        │
        └── Reserva
               │
               ├── Cliente
               │
               └── Pagamento
```

---

## Banco de Dados

O projeto utiliza modelagem relacional com:

- Chaves primárias
- Chaves estrangeiras
- Integridade referencial
- Restrições CHECK
- Relacionamentos 1:N
- Consultas JOIN complexas

---

## Como Executar

### 1. Clonar o Repositório

```bash
git clone https://github.com/seu-usuario/staymanager-hotel-system.git
```

### 2. Instalar Dependências

```bash
pip install psycopg2
```

### 3. Criar Banco de Dados

Execute:

```sql
Projeto BD.sql
```

no PostgreSQL.

### 4. Configurar Conexão

Edite:

```python
db_connection.py
```

informando:

```python
host
database
user
password
```

### 5. Executar

```bash
python test_crud.py
```

ou

```bash
python test_db.py
```

---

## Conceitos Aplicados

- Banco de Dados Relacional
- SQL Avançado
- CRUD Completo
- Integridade Referencial
- Modelagem Entidade-Relacionamento
- Consultas Analíticas
- Python Database API
- Persistência de Dados
- Relatórios Gerenciais

---

## Diferenciais do Projeto

- Sistema baseado em cenário real de hospedagem
- Estrutura preparada para expansão futura
- Consultas analíticas para gestão
- Relacionamentos complexos entre entidades
- Separação entre camada de acesso e operações
- Regras de integridade implementadas no banco

---

## Possíveis Evoluções (quem sabe, num futuro próximo...)

- API REST com Flask ou FastAPI
- Interface Web
- Dashboard administrativo
- Autenticação de usuários
- Relatórios em PDF
- Controle de disponibilidade em tempo real
- Integração com gateways de pagamento

---

## Autor

**Jordão Asato**

LinkedIn:
www.linkedin.com/in/jordao-asato-327063385

---
