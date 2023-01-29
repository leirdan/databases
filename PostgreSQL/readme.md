# 1. INTRODÇÃO AO POSTGRESQL

-   O PostgreSQL é um tipo de banco de dados relacional (SQL) que lida excepcionalmente bem com altos volumes de informação e consultas aos dados, garantindo um acesso rápido e seguro a tais informações. Além disso, é um projeto open-source.

# 2. COMO CRIAR UM BANCO DE DADOS POSTGRESQL

## 2.1 TABELAS

### 2.1.1 Mago

    - id_wizard (integer, pk)
    - name_wizard (varchar, 255)
    - wisdom (integer, 3)
    - intelligence (integer, 3)
    - birth_date (integer)
    - id_school (integer, foreign key)

### 2.1.2 Feitiço

    - id_spell (integer, pk)
    - name_spell (varchar, 100)
    - description (varchar, 255)
    - level (integer, 1)
    - id_category (integer, foreign key)

### 2.1.3 Categoria

    - id_category (integer, pk)
    - name_category (varchar, 100)
    - description (varchar, 255)

### 2.1.4 Escola

    - id_school (integer, pk)
    - name_school (varchar, 255)
    - principal (varchar, 255)
    - location (varchar, 255)

### 2.1.5 ListaFeitiços (tabela-pivô)

    - id_wizard (integer)
    - id_spell (integer)

## 2.2 REGISTRANDO NO BANCO

-   Abra o **pgAdmin 4**; na barra lateral, clique em **Servers**, então em **PostgreSQL 15** e em **Databases**;
-   Clique com o botão direito em Databases e escolha a opção "Create";
-   Defina o nome do banco de dados, o proprietário e outras opções adicionais e clique em "Save".

### 2.2.1 Inserindo comandos SQL

-   Para criar as tabelas e executar outras operações, vá em **Tools** e depois em **Query Tool**, onde será exibida uma janela para inserir os comandos.

### 2.2.2 Comandos usados para criar as tabelas

#### 2.2.2.1 Tabela "Wizard"

    CREATE TABLE Wizard (
    id_wizard integer serial primary key,
    name_wizard varchar(100) not null,
    wisdom integer(3) not null,
    intelligence integer(3) not null,
    birth_date integer,
    id_school integer,
    FOREIGN KEY (id_school) REFERENCES School (id_school)
    )

-   Vale notar que, para determinar um número que se auto incrementa, é usada a palavra reservada **serial** no atributo desejado.
-   A última linha faz o relacionamento entre esta tabela e a tabela "School" por meio de uma chave estrangeira "id_school".
