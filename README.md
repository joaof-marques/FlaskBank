# Projeto Sistema Bancário FlaskBank

## Autor: João Pedro Ramos Faustino Pereira Marques

Este é um projeto feito para o curso da Alpha EdTech de formação acelerada.
O projeto consiste em uma API REST feita em Python utilizando o framework Flask que simula um sistema bancário.
Nessa aplicação estão disponíveis os seguintes endpoints:

- Cadastrar Cliente
- Detalhar Perfil do Cliente
- Editar Perfil do Cliente
- Realizar depósito
- Realizar transferência entre contas
- Realizar saques
- Listar transferências realizadas
- Listar saques realizados
- Listar depósitos realizados
- Visualizar extrato completo


** Importante: O formato escolhido para retorno dos endpoints foi JSON, quando houver retorno**

**- Esta aplicação utiliza um banco de dados hospedado no ElephantSQL -**

**IMPORTANTE: No momento esta API ainda está em desenvolvimento e não foi hospedada em um servidor remoto. Quando isso acontecer, o link estará disponível nesta seção.


As entidades deste projeto são:

- Conta:
    - Nome: String
    - Id_conta: int
    - Saldo: float
    - Historico_transacoes: List[Transferencia]
    - Historico_saques: List[Saque]
    - Hitorico_depositos: List[Depósito]
    - CNPJ ou CPF: int

- Transferencia
    - id_conta_origem: int
    - id_conta_destino: int
    - Valor: float
    - Data: Date
    - id_transacao: int

- Saque
    - valor_saque: float
    - Data: Date
    - id_saque: int

- Depósito
    - valor_deposito: float
    - Data: Date
    - id_deposito: int


Abaixo estão os possíveis **_status codes_** de resposta desta API.
```python
# 200 (OK) = requisição bem sucedida
# 201 (Created) = requisição bem sucedida e algo foi criado
# 204 (No Content) = requisição bem sucedida, sem conteúdo no corpo da resposta
# 400 (Bad Request) = o servidor não entendeu a requisição pois está com uma sintaxe/formato inválido
# 401 (Unauthorized) = o usuário não está autenticado (logado)
# 403 (Forbidden) = o usuário não tem permissão de acessar o recurso solicitado
# 404 (Not Found) = o servidor não pode encontrar o recurso solicitado
```

## **Endpoints**

### **Cadastrar Cliente**

#### `Post /cliente`

Esta rota será utilizada para cadastrar novos clientes.
Para tal, será necessário enviar no corpo da requisição os seguintes dados:

```python
#{
#  - nome: String
#  - tipo_conta: String ("PJ" ou "PF")
#  - CNPJ ou CPF: int
#}
```

**Resposta**
Em caso de **sucesso**, a aplicação retornará no corpo da resposta um detalhamento da conta criada (Nome, CPF ou CNPJ, Saldo, Histórico de Transações, Histórico de Saques, Histórico de Depósitos).
Em caso de **falha** um status code apropriado será retornado explicando o motivo da falha.


### *** Detalhar Perfil do Cliente ***

#### `GET /cliente/id`

Esta rota será utilizada para visualizar os dados de um cliente cadastrado.

**Resposta**
Em caso de **sucesso**, a aplicação retornará no corpo da resposta um detalhamento da conta cadastrada (Nome, CPF ou CNPJ, Saldo, Histórico de Transações, Histórico de Saques, Histórico de Depósitos).
Em caso de **falha** um status code apropriado será retornado explicando o motivo da falha.

### **Editar Perfil do Cliente**

#### `PUT /cliente/id`

Esta rota será utilizada para atualizar os dados de um cliente cadastrado.
Para tal, será necessário enviar no corpo da requisição os dados que devem ser atualizados em formato JSON.

```python
#{
# - nome
# - cnpj ou cpf
#}
```

**Resposta**
Em caso de **sucesso**, a aplicação retornará no corpo da resposta um detalhamento da conta atualizada (Nome, CPF ou CNPJ, Saldo, Histórico de Transações, Histórico de Saques, Histórico de Depósitos).
Em caso de **falha** um status code apropriado será retornado explicando o motivo da falha.

### **Realizar Depósito**

#### `POST /deposito/id`

Esta rota será utilizada para depositar dinheiro na conta de um cliente.
Para tal, será necessário enviar no corpo da requisição os seguintes dados:


```python
#{
#  - id_conta_destino
#  - valor
#}
```


**Resposta**
Em caso de **sucesso**, a aplicação retornará no corpo da resposta um comprovante do depósito efetuado.
Em caso de **falha** um status code apropriado será retornado explicando o motivo da falha.

### **Realizar Transferência**

#### `POST /transferencia/id`

Esta rota será utilizada para realizar transferência entre contas cadastradas.
Para tal, será necessário enviar no corpo da requisição os seguintes dados:


```python
#{
#  - id_conta_destino
#  - valor
#}
```


**Resposta**
Em caso de **sucesso**, a aplicação retornará no corpo da resposta um comprovante da transferência efetuada, contendo informações da conta de origem.
Em caso de **falha** um status code apropriado será retornado explicando o motivo da falha.

### **Realizar Saque**

#### `POST /saque/id`

Esta rota será utilizada para realizar saques de uma conta cadastrada.
Para tal, será necessário enviar no corpo da requisição os seguintes dados:


```python
#{
#  - valor
#}
```

**Resposta**
Em caso de **sucesso**, a aplicação retornará no corpo da resposta um comprovante do saque efetuado, contendo informações da conta de origem.
Em caso de **falha** um status code apropriado será retornado explicando o motivo da falha.

### **Listar Transferências Realizadas**

#### `GET /transferencia/id`

Esta rota será utilizada para listar transferências feitas e recebidas de uma conta cadastrada.

**Resposta**
Em caso de **sucesso**, a aplicação retornará no corpo da resposta os dados da conta e o histórico das operações solicitadas.
Em caso de **falha** um status code apropriado será retornado explicando o motivo da falha.

### **Listar Transferências Realizadas**

#### `GET /saque/id`

Esta rota será utilizada para listar saques feitos em uma conta cadastrada.

**Resposta**
Em caso de **sucesso**, a aplicação retornará no corpo da resposta os dados da conta e o histórico das operações solicitadas.
Em caso de **falha** um status code apropriado será retornado explicando o motivo da falha.

### **Listar Depósitos Realizados**

#### `GET /depositos/id`

Esta rota será utilizada para listar depósitos feitos em uma conta cadastrada.

**Resposta**
Em caso de **sucesso**, a aplicação retornará no corpo da resposta os dados da conta e o histórico das operações solicitadas.
Em caso de **falha** um status code apropriado será retornado explicando o motivo da falha.

### **Visualizar Extrato Completo**

#### `GET /extrato/id`

Esta rota será utilizada para listar todas as operações feitas na conta selecionada (incluindo transferências, saques e depósitos), organizadas por ordem cronológica.

**Resposta**
Em caso de **sucesso**, a aplicação retornará no corpo da resposta os dados da conta e o histórico das operações solicitadas.
Em caso de **falha** um status code apropriado será retornado explicando o motivo da falha.