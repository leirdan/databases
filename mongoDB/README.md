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
