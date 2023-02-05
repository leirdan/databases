# 1. INTRODUÇÃO AO MONGODB

O MongoDB é um SGBD (Sistema Gerencial de Banco de Dados) do tipo NoSQL - ou seja, é não-relacional e não utiliza comandos do tipo SQL (como os do PostgreSQL, MySQL e outros). O MongoDB funciona da seguinte forma:

-   Cada "tabela" é chamada de **Collection** (coleção);
-   Cada conjunto de dados inserido numa Collection é chamado de **Document** (documento) e, muitas vezes, têm estruturas do tipo JSON;

    -   A estrutura de documentos permite que existam, dentro de um documento, outros documentos aninhados;
    -   Por exemplo:

    ```json
    {
    	"title": "mother tongue",
    	"year": 2019,
    	"genre": "pop rock",
    	"band": {
    		"name": "bring me the horizon",
    		"members": "...."
    	}
    }
    ```

    -   Neste caso, em uma Collection de "Songs" o seguinte documento detalhando uma música tem outro documento dentro de si, que detalha a banda que a compôs e tem propriedades próprias.
    -   Detalhe importante: cada documento de uma coleção tem um atributo **\_id** do tipo **ObjectId**, um identificador único de cada documento.

Dessa forma, as consultas de dados podem ser mais fáceis a depender do caso. O MongoDB também é um banco de dados bastante rápido.

# 2. INSTALANDO MONGODB NO WINDOWS 10

## 2.1 MongoDB e MongoDB Compass

-   Acesse o link "https://www.mongodb.com/try/download/" e procure na barra lateral "MongoDB Community Edition";
-   Ao clicar, escolha "MongoDB Community Server", escolha a versão do mongoDB, seu sistema operacional e o tipo de arquivo. Por fim, baixe-o;
-   Ao abrir o executável, prossiga até a tela de selecionar o setup e escolha uma das duas opções de acordo com suas necessidades (no meu caso, versão Complete);
-   Depois, habilite a checkbox "Install MongoDB as a Service" e prossiga;
-   Por fim, instale também o MongoDB Compass, a interface gráfica do MongoDB.

## 2.2 Mongo shell

    Mongo Shell é o terminal próprio do Mongo onde é possível executar comandos.

-   Acesse o link "https://www.mongodb.com/try/download/shell", escolha a versão do shell, seu sistema operacional
    e baixe o arquivo executável.
-   Após isso, execute o arquivo, dê um "next" em tudo e instale o shell do mongo.
-   Para acessar este terminal, abra o seu Powershell ou Prompt de Comando e digite **mongosh**. Após inserir este comando, será possível acessar o banco de dados MongoDB a partir do terminal.

# 3. MONGODB COMPASS

-   O Compass é uma interface do MongoDB onde é possível visualizar as coleções e documentos e realizar operações de forma mais visível e simplificada.

## 3.1 Conectar a um database

-   Existem duas opções iniciais no Compass:
    -   A primeira consiste em usar uma "connection string" (uma URL especial do MongoDB) para se conectar a uma database online, por exemplo, e interagir com ela a partir do Compass.
    -   A segunda (e que vou usar) é apenas clicar em "Connect" e deixar o campo da connection string vazio, pois assim o MongoDB Compass vai se conectar à sua máquina local, e não online.

## 3.2 Visualizando databases

-   Na página que foi aberta ao realizar a operação acima estarão listadas todas as databases que existem em seu computador. Por padrão, são criadas 3 databases: "admin", "config" e "local".
-   Para criar uma nova database, vá na barra "Databases", clique no ícone de "+" no fim da barra, defina o nome da database e pelo menos uma coleção. Após isso, clique em "Create Database" e sua database será criada.
-   Para deletar uma database, passe o _mouse_ por cima de seu nome e clique no ícone de lixeira.

## 3.3 Acessando databases e coleções

-   Clique em uma database para acessá-la. Dentro, serão listadas as coleções que fazem parte e, clicando em uma coleção, serão listados os documentos que fazem parte dela.
-   Para criar uma coleção em um banco de dados, clique em **Create Collection** já dentro da database desejada e insira seu nome.
-   Para deletar uma coleção, vá na barra lateral e, na database desejada, clique nas reticências que aparecem ao passar o _mouse_ por cima da coleção desejada e escolha **Drop Collection**.

## 3.4 Acessando documentos

-   Ao entrar em uma coleção, como dito, vão ser listados os documentos dela.
-   Para adicionar um novo documento, na aba "Documents", clique em **Add Data** e defina se o documento será um arquivo a ser importado ou se ele será escrito na hora.

    -   Ao escolher a opção **Insert document**, uma janela será exibida para você adicionar manualmente o documento. Ele deverá ser escrito como um objeto JSON, ou seja, baseado em pares de chave-valor (ex.: "nome": "cenoura"). Ao fim, clique em **Insert** para inserir o documento.
    -   Caso queira inserir mais de um documento simultaneamente, coloque um colchete "[]" abrindo e outro fechando todo o objeto antes das chaves "{}", e, a cada documento, coloque uma vírgula entre um e outro.

-   Para deletar, duplicar ou atualizar o documento, passe com o _mouse_ por cima dele e clique em um dos ícones que simboliza a operação desejada.

-   Para filtrar um ou mais documentos específicos, na barra de nome **Filter**, insira por qual campo do documento será feita a filtragem e qual o valor buscado na forma de um objeto JSON.
    -   Exemplo de busca: `{ autor: "George R.R Martin" }` -> retornará todos os documentos que tenham o valor "George R.R Martin" no campo de "autor".

# 4. MONGODB SHELL

-   Para acessar o terminal do mongodb, apenas digite **mongosh** no prompt de comando, Powershell ou outro terminal e tecle _enter_ para entrar.
-   Como forma de testar as operações e aprender a manipular o mongodb, vou utilizar o seguinte banco de dados:
    -   Database **Mercearia**
        -   Collection **Produtos**
            -   Campos dos documentos: **nome**, **preço (unitário)\*, **descrição**, **categoria**, **ncm\*\*;
        -   Collection **Clientes**
            -   Campos dos documentos: **primeiro nome**, **último nome**, **endereço**;

## 4.1 Comandos básicos

-   **help**: lista os comandos;
-   **cls**: limpa o terminal das informações anteriores;
-   **show dbs**: lista todas as databases criadas no seu computador;
-   **use mercearia**: troca para a database "mercearia" ou qualquer outra que você queira, basta apenas trocar o nome "mercearia" pela database desejada;
    -   Importante: você pode trocar para qualquer database, ela existindo ou não. Caso o faça, a database só será criada de fato quando inserir uma coleção nela.
-   **show collections**: exibe todas as coleções dentro da database;
    -   Importante: você pode, simultaneamente, criar uma coleção e inserir um documento dentro dela. Basta usar os comandos listados abaixo normalmente, já que um "db.clientes.insertOne({...})" é capaz de criar a coleção e o documento inserido.

## 4.2 Comandos de manipulação de documentos

### 4.2.1 Inserção

-   **db.produtos.insertOne({...})**: a função "insertOne()" insere um único documento na database, e esse documento é inserido na forma de um objeto JSON.
    -   O documento inserido foi:
    ```json
    {
        _id: ObjectId("63dfc81e13c95341ad23f5d9"),
        nome: 'arroz branco',
        'preço': 5,
        descricao: 'fino arroz branco da marca Lalilulelou',
        categoria: { descricao: 'alimentos perecíveis' },
        ncm: 100610
    }
    ```
-   **db.clientes.insertMany([{...}, {...}])**: a função "insertMany()" é capaz de inserir mais de um documento ao mesmo tempo.

    -   Documentos inseridos:

    ```json
    [
        {
            _id: ObjectId("63dfcd3213c95341ad23f5da"),
            primeiro_nome: 'François',
            ultimo_nome: 'Lacerda',
            'endereço': 'Rua dos Vagalumes, nº 42'
        },
        {
            _id: ObjectId("63dfcd3213c95341ad23f5db"),
            primeiro_nome: 'Augusto',
            ultimo_nome: 'Souza',
            'endereço': 'Avenida Barbeiro Barbosa'
        }
    ]
    ```

### 4.2.2 Listagem

-   **db.clientes.find()**: método que, inserido assim, retorna os 20 primeiros documentos de uma coleção. Caso queira buscar algum em específico, insira, entre os (), o campo e o valor desejado (exatamente como no Compass).

    -   Exemplo: buscar apenas o cliente "Augusto".

    -   `db.clientes.find({primeiro_nome: "Augusto"})`

-   Caso queira buscar somente alguns campos do documento, não todos, após chamar o método ".find()" defina um objeto vazio e, após ele, um outro objeto contendo apenas os campos que deseja selecionar seguidos do número 1.

    -   Exemplo: buscar apenas o primeiro nome de todos os clientes.

    -   `db.clientes.find({}, { primeiro_nome: 1 })`

-   **db.produtos.findOne({...})**: método que busca por um único documento a partir do campo e do valor passados como parâmetros.
    -   Exemplo: buscar somente o produto "cenoura".
        `db.produtos.findOne({nome: "cenoura"})`
