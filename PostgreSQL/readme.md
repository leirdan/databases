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
    birth_date date,
    id_school integer,
    FOREIGN KEY (id_school) REFERENCES School (id_school)
    )

-   Vale notar que, para determinar um número que se auto incrementa, é usada a palavra reservada **serial** no atributo desejado.
-   A última linha faz o relacionamento entre esta tabela e a tabela "School" por meio de uma chave estrangeira "id_school".

#### 2.2.2.2 Tabela "Spell"

    CREATE TABLE Spell (
    id_spell serial primary key,
    name_spell varchar(255) not null,
    description text not null,
    level smallint not null,
    id_category integer not null,

    FOREIGN KEY (id_category) REFERENCES Category (id_category)
    )

#### 2.2.2.3 Tabela "Category"

    CREATE TABLE Category (
    id_category serial primary key,
    name_category varchar(255) not null,
    description text
    )

#### 2.2.2.4 Tabela "School"

    CREATE TABLE School (
    id_school serial primary key,
    name_school varchar(255) not null,
    principal varchar(255) not null,
    place varchar(255)
    )

#### 2.2.2.5 Tabela-pivô "Wizard_Spell"

    CREATE TABLE Wizard_Spell (
    id_wizard integer not null,
    id_spell integer not null,

    FOREIGN KEY (id_wizard) REFERENCES Wizard (id_wizard),
    FOREIGN KEY (id_spell) REFERENCES Spell (id_spell)
    )

### 2.2.3 Inserir dados nas tabelas

#### 2.2.3.1 Criando uma nova Escola

    INSERT INTO School (name_school, principal, place) VALUES ('Gliamselv Tower', 'Gliaczan II', 'Kingdom of Faline')

-   O comando **insert into** requer o nome da tabela onde vão ser inseridos os dados (School), as colunas e seus respectivos valores; caso sejam do tipo string, devem ser escritos entre aspas simples.

#### 2.2.3.2 Criando um novo Mago

    INSERT INTO Wizard (name_wizard, wisdom, intelligence, birth_date, id_school) VALUES ('Leirdan', 14, 17, '17-02-2004', 1)

#### 2.2.3.3 Criando Categorias dos feitiços

    1. Ilusão: INSERT INTO Category (name_category, description) VALUES ('Illusion', 'Spells to deceive and confuse enemies minds.')
    2. Evocação: INSERT INTO Category (name_category, description) VALUES ('Evocation', 'Spells to evoke magical elements with high destructive power.')

#### 2.2.3.4 Criando novos Feitiços

    1. Change Self: INSERT INTO Spell (name_spell, description, level, id_category) VALUES ('Change Self', 'This spell enables the Illusionist to alter the appearance of his or her form - including clothing and equipment - to appear 1" shorter or taller; thin, fat, or in between; human, humanoid, or any other generally man-shaped bipedal creature. The duration of the spell is 2 to 12 (2d6) rounds base plus 2 additional rounds per level of experience of the spell caster.', 1, 1)
    2. Magic Missile: INSERT INTO Spell (name_spell, description, level, id_category) VALUES ('Magic Missile', 'Use of the Magic Missile spell creates one or more magical missiles which dart forth from the magic-users fingertip and unerringly strike their target. Each missile does 2 to 5 hit points (d4+1) of damage. If the magic-user has multiple missile capability, he or she can have them strike a single target creature or several creatures, as desired. For each level of experience of the magic-user, the range of his or her Magic Missile extends 1" beyond the 6" base range. For every 2 levels of experience, the magic-user gains an additional missile, i.e. 2 at 3rd level, 3 at 5th level, 4 at 7th level, etc.', 1, 2).
    3. INSERT INTO Spell (name_spell, description, level, id_category) VALUES ('Nystul"s Magic Aura', 'By means of this spell any one item of a weight of 50 g.p. per level of experience of the spell caster can be given an aura which will be noticed if detection of magic is exercised upon the object. If the object bearing the Nystul"s Magic Aura is actually held by the creature detecting for a dweomer, he, she or it is entitled to a saving throw versus magic, and if this throw is successful, the creature knows that the aura has been placed to mislead the unwary. Otherwise, the aura is simply magical, but no amount of testing will reveal what the magic is. The component for this spell is a small square of silk which must be passed over the object to bear the aura.', 1, 1)

#### 2.2.3.5 Quando um mago adquire um feitiço

    INSERT INTO Wizard_Spell (id_wizard, id_spell) VALUES (1, 2)

-   O mago com ID 1 (Leirdan) vai poder usar o feitiço "Magic Missile" (id 2) agora.

### 2.2.4 Edição de dados

    UPDATE School SET principal = 'Glakzan' WHERE principal = 'Gliaczan II'

-   Usa-se o comando **update** para definir a tabela, depois o **set** para definir o novo valor da coluna e **where** para definir onde será aplicada a atualização.

### 2.2.5 Excluindo um dado

    DELETE FROM Spell WHERE id_spell = 1

-   Usa-se o comando **delete** para especificar a operação, o **from** para definir qual a tabela que vai ser alvo da operação e **where** para definir a condição que a coluna deve atender para ser excluída.
-   Neste caso, será excluída a magia que tem o ID 1 ('Change Self').

## 2.3 CONSULTANDO O BANCO

### 2.3.1 Comando "SELECT"

#### 2.3.1.1 Consulta simples

    SELECT * FROM Spell

-   Essa consulta retorna todos as colunas com todos os campos (\*) da tabela Spell.

#### 2.3.1.2 Consulta de apenas uma coluna

    SELECT name_spell FROM Spell

-   Essa consulta retorna os valores de todas as colunas **name_spell** da tabela Spell.

#### 2.3.1.3 Consulta de duas ou mais colunas

    SELECT name_category, description FROM Category

-   Retorna os valores das colunas **name_category** e **description** da tabela Category.

#### 2.3.1.4 Uso de "ORDER BY"

-   Sem usar o "Order By", a listagem vai ser ordenada de acordo com as modificações; se uma linha teve um update, ela vai ser listada abaixo das que não tiveram, e assim em diante.

##### 2.3.1.4.1 Ordenação simples

    SELECT name_category, description FROM Category ORDER BY name_category ASC

-   Retorna os nomes das categorias ordenados em ordem alfabética, apenas.

##### 2.3.1.4.2 Ordenação de duas colunas

    SELECT name_wizard, intelligence, birth_date FROM Wizard ORDER BY name_wizard, intelligence

-   Retorna os nomes dos magos em ordem alfabética; caso hajam magos com o mesmo nome, a ordenação será feita a partir da coluna **intelligence** de forma ascendente - ou seja, em uma suposta situação, a listagem seria "Leirdan | 14" ; "Leirdan | 17"; "Lutz | 13"

#### 2.3.1.5 Uso de "WHERE"

     SELECT * FROM Category WHERE name_category = 'Illusion'

-   Retorna todos dos dados da categoria que for chamada "Illusion"

#### 2.3.1.6 Uso de "OR"

    SELECT * FROM Wizard WHERE wisdom = 14 OR wisdom = 13

-   Retorna os dados que tiverem a columa "wisdom" com valor 14 ou 13.
    -   Pode-se fazer quantos "OR" quiser.
